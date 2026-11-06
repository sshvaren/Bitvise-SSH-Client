# Bitvise SSH Client

## Introduction

Bitvise SSH Client is a Windows application designed for secure remote access, encrypted file transfers, and network tunneling through the Secure Shell (SSH) protocol. It provides a graphical interface for managing SSH connections while supporting command-line operations and automation. The application is commonly used by system administrators, network engineers, and developers who require authenticated access to remote servers and protected network resources.

The client supports password authentication, public-key authentication, and keyboard-interactive authentication, depending on server configuration. Public-key authentication enables administrators to establish connections without transmitting account passwords, making it suitable for controlled infrastructure environments. SSH host key verification helps detect unexpected changes in server identity and reduces the risk of connecting to unauthorized systems.

Bitvise SSH Client includes an integrated terminal for executing remote commands and an SFTP interface for transferring files securely. These functions allow administrators to inspect system logs, modify configuration files, deploy application components, and maintain remote directories within an encrypted session.

The application also supports SSH port forwarding, including local, remote, and dynamic forwarding. These capabilities enable encrypted access to services that are not directly exposed to external networks, such as internal databases, development environments, and administrative interfaces.

Connection profiles can store server addresses, authentication preferences, and session settings for repeated use. This simplifies access to multiple environments with different security requirements. For operational consistency, administrators can configure reusable profiles and integrate command-line connection handling into maintenance workflows, deployment procedures, and routine infrastructure administration tasks across distributed systems.

## Connection Configuration and Authentication

Before establishing a connection, verify that the target server runs an SSH service and that the required network port is reachable. SSH typically uses TCP port 22, although administrators may configure a different port for their infrastructure.

In the Bitvise SSH Client graphical interface, open the Login tab and configure the connection parameters:

1. Enter the target server's hostname or IP address in the Host field.
2. Specify the SSH service port in the Port field.
3. Enter the remote account name in the Username field.
4. Select the appropriate initial authentication method.
5. Click Log in to initiate the SSH connection.

For example, an administrator connecting to a Linux server at `192.168.10.25` can enter `admin` as the username and `22` as the port. Successful authentication establishes an encrypted session and allows access to the configured terminal and file-transfer functionality.

For public-key authentication, generate or import a compatible private key through the client key-management interface. Install the corresponding public key in the remote account's authorized keys configuration. Protect the private key with a passphrase and restrict access to its storage location.

During the initial connection, inspect the server's presented host key fingerprint and verify it against a trusted value obtained through an independent administrative channel. Unexpected fingerprint changes should be investigated before accepting the connection.

Save frequently used configurations as connection profiles to avoid repeated manual entry. Keep authentication secrets separate from shared profile files and use individual accounts for administrative accountability.

## Secure File Transfers and SSH Tunneling

Bitvise SSH Client provides integrated SFTP functionality for transferring files between Windows workstations and remote systems. SFTP operates within the encrypted SSH connection, protecting file contents and transfer-related operations from interception during transmission.

After authentication, open the SFTP window to display local and remote directory structures. Navigate to the required directories and transfer files using the graphical interface. Typical operations include uploading application configuration files, downloading diagnostic logs, and moving deployment packages to staging directories.

For example, an administrator can upload `app.conf` to `/opt/application/config/` before restarting an application service. Ensure that the destination account has appropriate write permissions and verify the transferred file before applying configuration changes. SFTP transfers do not automatically guarantee that remote application processes have reloaded modified files.

SSH tunneling provides another mechanism for accessing services through an encrypted connection. Configure forwarding rules in the Services tab before establishing the session.

With local port forwarding, a local TCP port connects to a destination accessible from the SSH server. For example, forwarding local port `15432` to `127.0.0.1:5432` on the remote server allows a database client to connect through the SSH tunnel using `127.0.0.1:15432`.

Dynamic forwarding creates a SOCKS proxy that forwards supported application traffic through the SSH connection. Remote forwarding exposes a client-side destination through a listening port on the SSH server, subject to server permissions.

Restrict forwarding rules to necessary interfaces and destinations. Close unused tunnels and terminate sessions when administrative operations are complete.
