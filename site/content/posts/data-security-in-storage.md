---
title: Data Security in Java
weight: 2
authors:
  - vijaywhat
authorimage: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSOd256TcC6vcaQ99TYzoP0pBbch9_Q-bbrmw&usqp=CAU'
---

Storage data security refers to the measures and techniques used to protect data from unauthorized access, modification, or destruction while in storage. Overall, storage data security is a critical component of protecting sensitive information, and organizations should implement a comprehensive security strategy that includes all of these components. Regularly monitoring, testing and updating the security measures will help to ensure that data is kept secure.

Crypytography is used to protect your sensitive data using one of the below

1. Pseudonymized
2. Anonymized
3. Generalized

These techniques can be used to detect data breaches and data leakages, and as an element of compliance, like in GDPR, HIPAA, and other regulations. This can help organizations to take steps to protect sensitive information and to prevent data breaches from occurring. Before we go to the techniques we need to understand

1. Plain Text
2. Cipher Text
3. Secret Key
4. Data de-identification converts plain text to cipher text by removing or obscuring personal identifying information from a plain text, making it less likely to be used to identify an plain text. 
5. Data identification - is the process of identifying plain text from cipher text.

## Pseudonymized (Encryption)
The term “pseudonymity” refers to using a different name on social media, such as a pen-name or nick-name. It is typically utilized to conceal your true identity while maintaining your identity under another name. Technically we call this technique as encryption

## Anonymity (Hashing)
In general, anonymity implies that no one is aware of your true identity, while they are undoubtedly aware of your online activity. It means that you can carry on with your movements while staying anonymous. Your actions and your true identity are kept separate by anonymity.Put simply, anonymity is a much stronger form of privacy than pseudonymity,Technically we call this technique as encoding. Eg. user passwords 

## Generalized
Generalization is the way of bucketing/masking the data as partial content. Eg. acoount number the last 4 digits

It is important to note that de-identifying data is not foolproof and there is always a risk of re-identification. Therefore, it's important to continuously monitor the data and to use multiple methods of de-identification to reduce the risk of re-identification.

Overall, data de-identification is a critical aspect of data privacy, and organizations should take the necessary steps to ensure that personal identifying information is removed or obscured in a way that effectively protects the privacy of individuals.

In addition to these methods, there are also several standards and frameworks that organizations can use to ensure that their data de-identification practices are effective. These include the Health Insurance Portability and Accountability Act (HIPAA) de-identification standard, the Safe Harbor Method, and the Statistical De-identification Method.

### Ref
1. https://www.gemini.com/cryptopedia/anonymity-vs-pseudonymity-basic-differences#section-what-does-a-pseudonym-mean-in-crypto
2. https://www.infoq.com/news/2023/01/aws-s3-default-encryption/
3. https://medium.com/@chintanaw/java-string-masking-performance-why-you-should-stop-worrying-and-rewrite-everything-in-c-849a79c04d0f
4. https://www.bbc.com/news/technology-60144498
5. https://www.baeldung.com/spring-security-5-default-password-encoder
6. https://github.com/p-h-c/phc-winner-argon2
7. https://www.twelve21.io/how-to-choose-the-right-parameters-for-argon2/