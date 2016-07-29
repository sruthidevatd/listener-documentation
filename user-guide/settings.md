Only users with administrative privileges will see **Settings** and other **ADMIN** options in the navigation panel.

Only users with Super User privileges will be able to log into **Settings**, also referred to as **System Settings**. The Super User is created when Listener is installed and is not an LDAP user.

From **System Settings**, you can perform the following tasks:

- View, create, edit, and delete LDAP domains
- Change system credentials (Super User password)

## Accessing System Settings

1. In the **ADMIN** navigation panel, click **Settings**.
2. In the **System Login** dialog, enter the **Admin Password** and then click **SIGN IN**.

## LDAP

**LDAP** is the default view and displays an LDAP card for each domain created.

### Viewing Domain Settings

1. Click the **LDAP** tab.
2. Click the card for the domain you want to view.

### Creating a Domain

1. Click the **LDAP** tab.
2. In the **LDAP Authentication** section, click the orange floating action button and do the following to set up authentication:
 1. Enter the **LDAP Connection Name**.
 2. Enter the **Server**. For example: `ldap.example.com`
 3. Enter the **Port**. For example: `389`
 4. Select an encryption option (**StartTLS**, **LDAPS**, or **None**).
 5. Enter the **Domain search user**. This is the LDAP user that authenticates other users when they log in. For example: `cn=ldap,ou=People,dc=listener,dc=com`
 6. Enter the **Domain search password**. This is the password for the **Domain search user**.
 7. Enter the **Domain base**. This is the starting point for all approved LDAP users. For example: `ou=People,dc=listener,dc=com`
2. In the **Map LDAP User Fields** section, enter the following to map information to your company's LDAP column names for user records:
 * **Name Field** (For example: `name`)
 * **Member of Field** (For example: `memberOf`)
 * **Email Field** (For example: `email`)
3. Click **TEST BEFORE SAVING**. A message appears indicating whether or not a connection was successful.
4. Do one of the following:
 * If the connection was successful, click **SAVE**.
 * If the connection was not successful, modify the settings, test again, and save the domain when the connection is successful.

### Editing a Domain

1. Click the **LDAP** tab.
2. Click the card associated with the domain you want to edit.
3. Make the desired changes.
4. Click **TEST CONNECTION**. A message appears indicating whether or not a connection was successful.
5. Do one of the following:
 * If the connection was successful, click **SAVE**.
 * If the connection was not successful, adjust the settings, test them again, and save them when the connection is successful.

### Deleting a Domain

1. Click the **LDAP** tab.
2. Click the card associated with the domain you want to delete.
3. In the lower right, click the trash can button. A delete confirmation message appears.
4. Click **DELETE**.

## SYSTEM CREDENTIALS

Use the **SYSTEM CREDENTIALS** tab to change the Super User password.

### Changing the Super User Password

1. Click the **SYSTEM CREDENTIALS** tab.
2. Click **CHANGE PASSWORD**.
3. In the **New password** box, enter the new password.
4. In the **Repeat New password** box, enter the new password again.
5. Click **SUBMIT**.
