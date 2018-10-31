# kinetic-sandbox-utils

Tools to use with Cisco's cloud managed platform ciscokinetic.io.

## Purpose

This code is not intended to end customer or typical production users. Instead it is mainly used for those willing to provide a flexible demonstration and learning playground, be them Cisco or Cisco partners.

## kinetic-sandbox-copy.py

The purpose of this program is to copy non-admin users from one Kinetic Cloud organisation, to another organisations as admin users. A new organisation will be created per user so that they can be king of their domain. The use-case for this program is extremely narrow and mostly used when giving training, however the usage of Cisco Kinetic Cloud API can be interesting for others.

To get help on options and argument for this program, invoke help:

<code>
python kinetic-sandbox-copy.py -h
</code>

Step by step, the program will:

 - Connect to Cisco Kinetic Cloud using your username and password. Password can be passed as an argument with <code>--password</code>, otherwise it will be interactively prompted.
 - List users in the source organisation, and for each user that is not an administrator, progrm will ask if the user needs to be copied. Either answer yes/no for each user, or use option <code>--all</code> to copy them all without asking.
 - For each user, an organisation will be created as a children of the destination organisation passed as an argument. The name of that organisation if the full name of the user followed by a fixed 5-char hash derived from the email address (to avoid risk of collision with [namefellows](https://en.wiktionary.org/wiki/namefellow)).
 - The user will be added to the newly created organisation as an administrator user. Because the user is alone, there is no risk of messing anything.

## Caveats and Known Issues

- Because the Cisco Kinetic Cloud is using paginated APIs, and this program has not implemented pagination yet, only the first 25 users of the source organisation will be considered (be them admin or not).
- The program does not take care of removing the organisation, so when you're done with the lab, delete them from the Cisco Kinetic Cloud user interface.
- If the script has been executed before, and the destination organisation already exists, this will raise an error. The script will ignore this user and carry on. There is no API to check if an organisation exists by name, only by number.

## Warranty and support

These tools are provided 'as-is' with no support even if I'll do my best to take requests into account. On the other side I always appreciate pull requests.

--- Emmanuel
