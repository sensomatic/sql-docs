---
title: "SQL Server Certificates and Asymmetric Keys | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: sql
ms.prod_service: "database-engine, sql-database, sql-data-warehouse, pdw"
ms.reviewer: ""
ms.technology: security
ms.topic: conceptual
helpviewer_keywords: 
  - "security [SQL Server], certificates and asymmetric keys"
ms.assetid: 8519aa2f-f09c-4c1c-96b5-abc24811e60c
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# SQL Server Certificates and Asymmetric Keys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 Public Key Cryptography is a form of message secrecy in which a user creates a *public* key and a *private* key. The private key is kept secret, whereas the public key can be distributed to others. Although the keys are mathematically related, the private key cannot be easily derived by using the public key. The public key can be used to encrypt data which only the corresponding private key will be able to decrypt. This can be used for encrypting messages to the owner of the private key. Similarly the owner of a private key can encrypt data which can only be decrypted with the public key. This use forms the basis of digital certificates in which information contained in the certificate is encrypted by the owner of a private key, assuring the author of the contents. Since the encrypting and decrypting keys are different they are known as *asymmetric* keys.
  
 Certificates are a format containing the owner's public key, the issuer's signature and other information such as expiry dates and distinguished names of the owner and issuer. The issuer's signature is information in the certificate that is encrypted - also known as signed - by the issuer's private key. If the issuer and owner are different on one certificate then to verify this certificate the issuer's public key must be used to decrypt the signed information. This public key will be on another certificate where the first issuer is the owner. This second certificate may also have a different issuer, and so a third certificate must be available to verify the first two. This process is followed until a certificate where the issuer and owner are the same is reached. This forms a certificate chain. This final certificate, and hence the entire chain will be trusted if it matches one of a set of known certificates, known as root certificates, which are securely distributed to the operating environment. If the final certificate cannot be identified against this trust store, it is treated as self-signed and not trusted. This is known as a chain of trust, and the whole system forms a Public Key Infrastrucutre (PKI).
 
 Certificates may contain the signed hash of a codebase to verify code integrity and authorship, or the public key in a certificate can be used to encrypt a symmetric key used for storage in a database.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contains features that enable you to create and manage certificates and keys for use with the server and database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cannot be used to create and manage certificates and keys with other applications or in the operating system.  
  
## Certificates  
 A certificate is a digitally signed security object that contains a public key for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. You can use externally generated certificates or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can generate certificates.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificates comply with the IETF X.509v3 certificate standard.  
  
 Certificates are useful because of the option of both exporting and importing keys to X.509 certificate files. The syntax for creating certificates allows for creation options for certificates such as an expiry date.  
  
### Using a Certificate in SQL Server  
 Certificates can be used to help secure connections, in database mirroring, to sign packages and other objects, or to encrypt data or connections. The following table lists additional resources for certificates in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Topic|Description|  
|-----------|-----------------|  
|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)|Explains the command for creating certificates.|  
|[Identify the Source of Packages with Digital Signatures](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)|Shows information about how to use certificates to sign software packages.|  
|[Use Certificates for a Database Mirroring Endpoint &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|Covers information about how to use certificates with Database Mirroring.|  
  
## Asymmetric Keys  
 Asymmetric keys are used for securing symmetric keys. They can also be used for limited data encryption and to digitally sign database objects. An asymmetric key consists of a private key and a corresponding public key. For more information about asymmetric keys, see [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md).  
  
 Asymmetric keys can be imported from strong name key files, but they cannot be exported. They also do not have expiry options. Asymmetric keys cannot encrypt connections.  
  
### Using an Asymmetric Key in SQL Server  
 Asymmetric keys can be used to help secure data or sign plaintext. The following table lists additional resources for asymmetric keys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Topic|Description|  
|-----------|-----------------|  
|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)|Explains the command for creating asymmetric keys.|  
|[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)|Displays the options for signing objects.|  
  
## Tools  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] provides tools and utilities that will generate certificates and strong name key files. These tools offer a richer amount of flexibility in the key generation process than the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] syntax. You can use these tools to create RSA keys with more complex key lengths and then import them into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. The following table explains shows where to find these tools.  
  
|||  
|-|-|  
|Tool|Purpose|  
|[makecert](http://msdn2.microsoft.com/library/bfsktky3\(VS.80\).aspx)|Creates certificates.|  
|[sn](http://msdn2.microsoft.com/library/k5b5tt23\(VS.80\).aspx)|Creates strong names for symmetric keys.|  
  
## Related Tasks  
 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
## See Also  
 [sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)   
 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
