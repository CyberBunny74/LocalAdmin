# Local Administrator Group Audit Tool

## Overview

This PowerShell script is designed to audit the membership of local administrator groups on client computers within a network. It's a valuable tool for IT administrators and security professionals to maintain oversight of local administrator privileges, enhancing an organization's security posture by identifying and managing administrative access rights.

## Features

- Search for computers in a specified Organizational Unit (OU) or query a specific computer by name
- Check membership of the local administrators group on each computer
- Exclude specified accounts from the results
- Generate a CSV report of non-excluded accounts with local admin privileges
- Filter out inactive computers based on a specified time frame

## Prerequisites

- Windows PowerShell 5.1 or later
- ActiveDirectory PowerShell Module
- Appropriate permissions to query Active Directory and perform remote WMI queries on target computers

## Usage

### Parameters

- `-ou`: Specifies the OU to search for computers
- `-excludeNames`: Array of account names to exclude from the results
- `-activeDays`: Number of days to consider a computer active
- `-pcName`: Specific computer name to query

### Examples

1. Search for computers in a specific OU:
   ```powershell
   .\LocalAdminGroupAudit.ps1 -ou "ou=myOU,ou=myCompany,dc=myDomain,dc=com" -excludeNames "Administrator","Domain Admins" -activeDays 30
   ```

2. Query a specific computer:
   ```powershell
   .\LocalAdminGroupAudit.ps1 -pcName PC01 -excludeNames "Administrator","Domain Admins"
   ```

## Output

The script generates a CSV report (`localadmins.csv`) in the `c:\csvreports\` directory, containing the following information:
- Computer Name
- Username with local admin rights
- Group Name

## Security Considerations

- Ensure that the account running this script has the necessary permissions to query Active Directory and perform remote WMI queries.
- Review and update the `-excludeNames` parameter regularly to maintain an accurate list of authorized admin accounts.
- Handle the output CSV file securely, as it contains sensitive information about administrative access.

## Limitations

- The script requires remote WMI access to target computers, which may be blocked by firewalls or security policies in some environments.
- Performance may be impacted when running against a large number of computers.

## Contributing

Contributions to improve the script are welcome. Please fork the repository and submit a pull request with your proposed changes.

## License

[MIT License](LICENSE)

## Disclaimer

This script is provided as-is, without any warranties or guarantees. Always test in a non-production environment before using in a production setting.
