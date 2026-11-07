# IMAP Mail Cindy Plugin

[![GitHub](https://img.shields.io/badge/GitHub-nobleits88%2Fimap--mail--cindy-181717?logo=github)](https://github.com/nobleits88/imap-mail-cindy)

IMAP Mail is a Cindy Plugin for managing configured email mailboxes through IMAP and SMTP.

**GitHub:** https://github.com/nobleits88/imap-mail-cindy

## Features of the Plugin

- Read recent messages from configured IMAP mailboxes.
- List mailbox folders, including special-use folders when reported by the server.
- Inspect message authentication and routing details for spam or phishing review.
- Move messages between folders.
- Delete messages by moving them to the server's Trash folder.
- Send new email messages through the configured SMTP server.
- Reply to existing messages with threading support.
- Forward messages inline or as `.eml` attachments.
- Support multiple mailboxes, up to 16 configured accounts.
- Configure separate IMAP and SMTP hosts, ports and security modes per mailbox.
- Support IMAP SSL and unencrypted connections.
- Support SMTP SSL, STARTTLS and unencrypted connections.
- Use SMTP port `465` as the default in the setup page.
- Store mailbox passwords in Cindy's secure host vault rather than normal settings metadata.
- Check email addresses for duplicates before adding them.
- Keep Gmail and other read-only mailbox workflows separate from write operations.

### Safety features

- Reading and inspection are read-only operations.
- Moving, deleting, sending, replying and forwarding require confirmation.
- Passwords, app passwords, tokens and verification codes are never requested in chat.
- Passwords must not be committed to GitHub or included in issue reports and release notes.

## How to Use the Plugin

### 1. Configure a mailbox

1. Install and enable the Plugin in Cindy.
2. Open the **IMAP Mail Plugin settings**.
3. Enter the email address and password or app password.
4. Enter the IMAP host, port and security mode.
5. Enter the SMTP host, port and security mode if sending is required.
6. Click **Add mailbox**.

The setup page uses an email-derived internal mailbox ID, so no separate short name is required. If the email address already exists, the Plugin rejects it instead of creating a duplicate.

For Gmail, use an appropriate **App Password** when required by the account's security settings. Enter it only through the secure Plugin settings page.

### 2. Read recent email

Ask Cindy to use `mail_recent`, optionally specifying:

- `account`: the configured mailbox ID
- `days`: number of days to search back, from 1 to 7
- `max`: maximum number of messages to return

Each result includes a message UID that can be used with inspection or message-management tools.

### 3. List folders

Use `mail_list_folders` with an optional `account` to view folders such as Inbox, Sent, Archive, Trash and Junk when the server reports them.

### 4. Inspect a message

Use `mail_inspect` with the message `uid` and optional folder to review:

- SPF, DKIM and Authentication-Results
- Reply-To mismatches
- Routing hops
- Links
- A text preview

### 5. Move or delete messages

Use `mail_move` to move selected UIDs to another folder. Use `mail_delete` to move selected messages to the server's Trash folder. These operations require confirmation.

### 6. Send, reply or forward

- `mail_send` sends a new plain-text message.
- `mail_reply` replies to a message and preserves threading headers.
- `mail_forward` forwards a message inline or as an `.eml` attachment.

These operations require confirmation of the exact recipients and content.

## Installation of the Plugin

### Install from a Cindy Plugin package

1. Download the latest `.cindy` package from the [GitHub repository](https://github.com/nobleits88/imap-mail-cindy/releases) or obtain it from the Plugin maintainer.
2. In Cindy, open the Plugin management screen.
3. Choose **Install Plugin** or the equivalent local-package installation action.
4. Select the `.cindy` package.
5. Enable **IMAP Mail** after installation.
6. Open the Plugin settings and configure at least one mailbox.

### Install from source for development

The repository contains the Plugin source, including `ghost.json`, `main.js`, the Node worker and the settings page. Use Cindy's local Plugin development or package-install workflow for the checked-out directory.

The source package requires:

- Cindy Plugin schema `3`
- Cindy `0.1.115` or newer
- A configured IMAP/SMTP mailbox

Do not run the Plugin without configuring a mailbox. A fresh installation does not contain a usable personal mailbox or password.

### Updating

When updating an existing installation, install the newer `.cindy` package over the existing IMAP Mail instance. Existing mailbox configuration and vault data should be preserved by Cindy. Recheck the settings page after updating if a mailbox appears unavailable.

## Available Tools

| Tool | Purpose |
| --- | --- |
| `add_mailbox` | Check an email address and direct the user to Plugin settings for setup |
| `mail_recent` | Read recent Inbox messages |
| `mail_list_folders` | List IMAP folders |
| `mail_inspect` | Inspect authentication, routing and content indicators |
| `mail_move` | Move messages between folders |
| `mail_delete` | Move messages to Trash |
| `mail_send` | Send a new email |
| `mail_reply` | Reply to an email |
| `mail_forward` | Forward an email |

## Security and Privacy

Never place mailbox passwords, Gmail App Passwords, SMTP credentials, tokens or verification codes in GitHub, README files, chat messages or issue reports. Configure credentials only through Cindy's secure Plugin settings flow.

## License

See the repository for the applicable license and contribution terms:

https://github.com/nobleits88/imap-mail-cindy
