## Encryption.

#### Foundations of designing Cryptographic Systems:
- A system is only as strong as its weakest link.
- All systems must be designed and build to be attacked (adversarial setting).
- Cryptography is very difficult.
- Cryptography is not the solution to a security problem, but it might be part of one.
- Complexity is still the enemy of security.
- The security of the Encryption system should only ever rest on the secrecy of the Encryption Key and not the Secrecy of the Encryption Algorithim.

### Message Encryption:
#### Symmetric Encryption:
- Basics of Secret Key Cryptography:
        - Alice wants to communicate with Bob.  
        However she does not want Eve to be able to receive the plain text message (M).
        Alice (M)----------> Eve (M) -------------> Bob (M)
        - Alice and Bob exchange a secret encryption key (Ke) which Alice uses to encrypt her message to Bob to produce Cypher text (Ct).
        Alice (E(M + Ke)) = Ct -----------> Eve (Ct)--------------->  Bob D(Ct + Ke) = M
        Eve can now only get access to the Cypher text of the message Alice is sending to Bob.

- The issue of Authentication.
        - Eve does not want Alice and Bob to communicate. So she sets out to change the message that Bob is receiving from Alice (M) with her own message (M1).
        - Alice (M) --------------> (M) Eve: (M1) --------------------> Bob (M1)
        - Alice now uses an agreed upon Key to compute a Message Authentication Code from her message using Bob's and her shared Key and sends it to Bob with the original message.
        - Alice (h(Ka, M) = (M, A))  ----------------> Eve (M, A)-------------------> Bob (M, A). Bob then generates his own Authentication code and compares it to the one he received (h(Ka, M)=A1 A==A1.
        - Now if Eve was to alter the original message (Mpt)= (Mpt1). Bob will be able to tell as the result of his Message Authentication Code (A1) will be different to Alices (A).
        -Alice (h(Ka, M) = (M, A))  ----------------> Eve (M1, A)-------------------> Bob (M1, A). h(Ka, M1)=A1. A!=A1.


##### Asymmetric Encryption: Public Key Cryptography
- The problem of Key exchange.
  - The problem remains that Alice and Bob need to exchange their secret key and they need to do it in a way that Eve cannot get access to it. What is Alice and Bob don't have any safe method to exchange keys?
  - Public Key Cryptography allows Alice to generate two Keys, a Public Key and a Private Key. Alice makes sure her Private Key is secret and safe.
  - Alice then sends her Public Key to Bob, she hosts it on the internet so people she doesn't know can get access to it. She gets Bob to do the same.
          - Now when she wants to communicate with Bob she simply encrypts her message with Bob's public key.
          - Alice also worried about Authentication makes sure she signs her message with her Private Key.
          Alice A(M,K(aliceprivate)) = Ma and then E(Ma, K(bobpublic)) = Ct
          Alice(Ct) ----------------> Eve(Ct) -----------------> Bob(Ct)
          - Bob then uses their private key to decrypt the message that was encrypted with their private key.
          D(Ct, K(bobprivate)) = Ma
          - After that bob checks the Authentication of Alice's message with Alice's public key to make sure the signature is good.
          A(Ma, K(alice public))

  - Because the messages are encrypted with the public key and decrypted with the private key, anyone can send an encrypted message that only the owner of the private key can read.
  - Also because the messages are authenticated with a users private key, but checked with their public key, anyone can confirm the message is from the owner of the private key.


- The problem of speed and size.
  - Because the system of Public Key Cryptography  does not rely on a secret key, the encryption keys must be much much bigger then in secret key Cryptography
  (4096bits for RSA as opposed to 256bits for AES). As a result speed is lost in public key cryptography.
  - Many real world encryption processes (such as HTTPS) use a combination of public key and secret key cryptography. The public key cryptography is used to safetly exchange a secret key that then encrypts all future exchanges.
  - However many messaging protocols (GPG, Signal and OTR) use public key cryptography.

### Device Encryption.
- There are two common ways to encrypt your devices. File encryption and Full Disk encryption. Each method has its own advantages. The general recommendation is that where possible attempt full disk encryption, such as for computers and external storage. Many phones have factory encryption schemes that decide for you.

##### Full Disk Encryption:
- Encrypts all the data on a drive, including the computer operating system and boot loader. Meaning all information added to the drive is encrypted by default. The Encryption key is then stored on the device and accessible to the user with the input of a password. When implemented correctly nothing is ascertainable about what is on the drive, like how much information, the type or structure of the drive.
  - Does not protect against intrusion of computer when on.
  - Does not protect data in transit or removed from encrypted device.
  - Requires user to limit access to device when networked through firewalls etc.

##### File System Encryption
- Can be used to create encrypted directories, vaults and files. Offers some protection against attack via networks.
  - Does not hide file system metadata. Like volume of the encrypted files, location or directory location.
  - Does not protect information that is not intentionally added to the encrypted file system.


#### The Power of Physics vs the world.
- When it (usually) wins:
  - Against Interception and and stored communications access.
  - Against malicious device access.
  - Against some forms of metadata such as browsing history, IP recording.


- When it loses:
  - The court may have some power to subpoena passwords to access 'evidence'.
  - If you do not give you password to ASIO when subpoened you face a 2 year prison sentence.
  - Against the Rubberhose: We can hold out as long as we want but sometimes the cost of not cooperating leads us to comply.
  - Against some forms of metadata, such as network analysis.
