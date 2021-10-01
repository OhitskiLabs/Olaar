OhitskiLabs AWS Assume Role Script
----------------------------------

#### Description
Cuts down on some AWS CLI role assumption annoyances by automatically setting the newly assumed role to the CLI's default profile within ~/.aws/credentials. Olaar's 'revert' command swaps the default AWS context back to the provided profile. Role assumption via Olaar supports an optional external id and uses the current AWS profile's account id to determine the assumed role ARN (account id can be overriden with the --account-id flag). If the external id is specified as an empty string, Olaar will prompt for the id to be entered, (e.g., --external-id ''). Please note that MFA is not supported if trust policies require supply an MFA device's serial number / arn and token.

---

#### Usage
Usage differs slightly on whether Olaar will be used to assume a role or revert back to a saved profile. Examples are probably the easiest way to demonstrate:
```bash
# Assumes role to arn:aws:iam::{AccountId}:assumed-role/MyRoleToAssume/{username}-{YYYY-MM-DD}
# And sets the aws_access_key, aws_secret_access_key, and aws_session_token in ~/.aws/credentials
python3 olaar.py assume --role MyRoleToAssume
```
```bash
# Assumes role to arn:aws:iam::123456789012:assumed-role/MyRoleThatRequiresExternalId/{username}-{YYYY-MM-DD}
# And sets the aws_access_key, aws_secret_access_key, and aws_session_token in ~/.aws/credentials
python3 olaar.py assume --role MyRoleThatRequiresExternalId --account-id 123456789012 --external-id ''
    External-Id: {input}
```
```bash
# Sets the default AWS profile to match what is specified for [MyStandardProfile] within ~/.aws/credentials
python3 olaar.py revert --profile MyStandardProfile
```

---

#### Requirements
Olaar requires argparse and boto3. Install the dependencies if you do not already have them with one of the two following lines:
```bash
python3 -m pip install argparse boto3
# Or
python3 -m pip install -r requirements.txt
```