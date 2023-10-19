# ArgoCD Helper

## Add a repository

```
#!/bin/bash

# Default Values
NAMESPACE="argocd" # can be openshift-gitops or other stuff depend on your installation
NAME=""
REPO_URL=""
REPO_URL=""
USERNAME=""
PASSWORD=""

# Parse command-line arguments
while getopts ":n:u:U:P:" opt; do
  case $opt in
    n) NAME="$OPTARG" ;;
    u) REPO_URL="$OPTARG" ;;
    U) USERNAME="$OPTARG" ;;
    P) PASSWORD="$OPTARG" ;;
    \?) echo "Invalid option -$OPTARG" >&2
        exit 1
        ;;
    :) echo "Option -$OPTARG requires an argument." >&2
       exit 1
       ;;
  esac
done

# Validate that mandatory options are provided
if [[ -z "$REPO_URL" || -z "$USERNAME" || -z "$PASSWORD" ]]; then
    echo "Usage: $0 -u <repo_url> -U <username> -P <password> [-n <name>]"
    exit 1
fi

# Base64 encode the values
ENCODED_NAME=$(echo -n "$NAME" | base64)
ENCODED_URL=$(echo -n "$REPO_URL" | base64)
ENCODED_USERNAME=$(echo -n "$USERNAME" | base64)
ENCODED_PASSWORD=$(echo -n "$PASSWORD" | base64)
TRUE64=$(echo -n "true" | base64)
FALSE64=$(echo -n "false" | base64)

# Create the secret
cat <<EOF | oc apply -n $NAMESPACE -f -
apiVersion: v1
kind: Secret
metadata:
  name: repo-$NAME
  labels:
    argocd.argoproj.io/secret-type: repository
type: Opaque
data:
  name: $ENCODED_NAME
  url: $ENCODED_URL
  username: $ENCODED_USERNAME
  password: $ENCODED_PASSWORD
  insecure: $FALSE64
  insecureIgnoreHostKey: $FALSE64
EOF

echo "Secret 'monrepo-secret' created/updated in namespace '$NAMESPACE'."
```
