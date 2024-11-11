john 
```bash
john --format=raw-sha256 --incremental hash3.txt
```
john --show 


NTHash is **the currently used algorithm for storing passwords on windows systems**. NTHashes of passwords are stored in NTDS.dit ( database for Active Directory environments), also in the Security Accounts Manager (SAM) database. You're going to need administrator access over the domain controller.




# John
# Creating Custom Rules in John the Ripper

Custom rules are defined in the `john.conf` file. You can find this file in the following locations:

- On the TryHackMe Attackbox: `/opt/john/john.conf`
- If installed via a package manager or built from source: `/etc/john/john.conf`

## Syntax of Custom Rules

1. **Define the Rule Name**  
   Use the following format to define your rule:
Replace `RuleName` with a name you choose for your custom rule.

2. **Modifiers**  
You can modify words using regex-style patterns. Here are some common modifiers:

- **Az**: Appends characters to the end of the word.
- **A0**: Prepends characters to the beginning of the word.
- **c**: Capitalizes the character at a specific position.

3. **Character Sets**  
You define the characters to append, prepend, or include in square brackets `[]` and double quotes `""`. Common examples:

- `[0-9]`: Includes numbers 0-9.
- `[0]`: Includes only the number 0.
- `[A-z]`: Includes both upper and lowercase letters.
- `[A-Z]`: Includes only uppercase letters.
- `[a-z]`: Includes only lowercase letters.
- `[!]`: Includes the symbol `!`, etc.

### Example Rule

To generate a wordlist that matches the password `Polopassword1!`, assuming the base word `polopassword` is in your wordlist, create a rule entry like this:

```plaintext
[List.Rules:PoloPassword]
cAz"[0-9] [!£$%@]"
```
**Explanation of the Example:**

- `c`: Capitalizes the first letter.
- `Az`: Appends characters to the end of the word.
- `[0-9]`: Appends a number in the range 0-9.
- `[!£$%@]`: Appends one of the symbols: `!`, `£`, `$`, `%`, or `@`.

## Using Custom Rules

To use your custom rule, call it with the `--rule` flag. Here’s the full command:

bash

Copy code

`john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]`

## Additional Tips

- Speaking out the patterns while writing a rule can help, just like when writing RegEx patterns.
- Jumbo John comes with many custom rules already available (check around line 678) if you need examples or get stuck with syntax.


For cracking the zip password 
**zip2john**
converts the zip hash to txt and used the obtained txt file to get the password

use case 
```bash
zip2john secure.zip >secure.txt
john --wordlist=rockyu.txt secure.txt
```
