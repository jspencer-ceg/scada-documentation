####################
1Password Guidelines
####################

1Password is a tool that we use to store credentials. The credentials can be for devices on projects and services that we use. 1Password keeps the passwords secure and accessible to members of the team from wherever they are. Each team member who has an account with CEG's 1Password account also receives a personal 1Password account. You can store your personal passwords to your personal 1Password account and store CEG-related passwords to the CEG 1Password account.

An indivdual record in 1Password is called an item. Items can be logins, identities, SSH keys, server information, software licenses, or anything else that needs to be stored securely.

Accounts
========

If you don't have an account, either Nick or Matt can create one for you.

Vaults
======

Items are stored in vaults. Think of them as folders. Each vault can have its own permissions settings that define how they are shared either within CEG or with outside parties. In the CEG account, there are three main types of vaults:

   :Employee: This is the vault where you can keep your own personal work-related items. Things like credentials for your SEL account, Outlook account, Beckwith Electric account, and other such things would be well suited here. This account is only accessible by you and is not shared with other team members.

   :Shared: This is the vault where we keep items that we share with the team. It includes any device credentials that we create for devices on site or in the SCADA lab. The permissions are set so that everyone on the team has access to these items.


   :Client vaults: These are vaults to store credentials that can be shared with the client. Each of these vaults is named with the client's name. They can be set up so that the client has access to these credentials at any time. **Update verbage to mean any external party that we work with**

   :Special-purpose vaults: These are vaults that you can create for special purposes and can be shared with the team, or not.

Items
=====

1Password has many different types of items to choose from. Here are a few of the major items that you'll be using most of the time and how to use them.

   :Login: This is the workhorse of items. A login is set up to store a username, password, and a website. Website logins, like SEL, or logins for devices that have web interfaces would be stored in a login item.

   :Password: This stores only a username and password. If something is really generic, it could be stored with a password item.

   :Server: You can store logins for servers in a server item. It has default fields for a URL (or an IP address), a username, and a password. There are other default fields in this item that keep track of things that we don't really use.

Fields in any item can be customized. As we use 1Password more, we may find ways that we can use custom fields. Custom fields should be used in a consistent way. Consult with Nick if you find a way to use custom fields that you think could be standardized across the board. The specifications for how those are used would be listed here.

Naming and Tagging
==================

Names should describe an item in such a way that it can be easily found by search. Care should be taken to name items in a consistent manner.

Case
----

Titles of items shall be in Title Case.

Name
----

The need for consistent structure is the greatest for items that describe device logins. The title should include, in this order:

#. Site name
#. Device number(s)
#. Model number

The format is :samp:`{SITE_NAME} {DEVICE_NUMBERS} {MODEL_NUMBER}`, where:

- :samp:`{SITE_NAME}` is the name of the site in Title Case. Be consistent and use the same version of the site name across all items related to a site
- :samp:`{DEVICE_NUMBERS}` is the device number for the device, as assigned in the drawings. If the item relates to more than one device, this becomes a comma-separated list. Use spaces between each item.
- :samp:`{MODEL_NUMBER}` is the model number for the device.

The following is a list of examples illustrating this format:

- High Lonesome 16ERFC-2 SEL-3620
- High Lonesome 16ESM-1, 16ESM-2, 16ESM-3 SEL-2730M

There is no need to put the username in the title, even if there are multiple accounts for a device. The username appears in a very clear way when the accounts are listed in 1Password.

Tags
----

If an item is related to a site, tag it with the name of the site. There should be only one tag per site. Tags shall be written in Title Case. Use the same name for the site as you use in the name of the item.
