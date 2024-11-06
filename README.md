# Stored-XSS-LibreNMS-Display-Name

**Description:**


XSS on the parameters (Replace $DEVICE_ID with your specific $DEVICE_ID value):`/device/$DEVICE_ID/edit` -> param: display


of Librenms version 24.9.0 ([https://github.com/librenms/librenms](https://github.com/librenms/librenms)) allows remote attackers to inject malicious scripts. When a user views or interacts with the page displaying the data, the malicious script executes immediately, leading to potential unauthorized actions or data exposure.


**Proof of Concept:**
1. Add a new device through the LibreNMS interface.
2. Edit the newly created device by going to the "Device Settings" section.
3. In the "Display Name" field, enter the following payload: `"><script>alert(1)</script>`.
![Screenshot from 2024-11-06 09-41-37](https://github.com/user-attachments/assets/6b44e049-5748-4f70-a667-c681cacec9da)

4. Save the changes.
5. The XSS payload triggers when navigating to either the "Alert Rules" or "Custom OID" sections within the "Edit" tab for the device. Additionally, if an application was previously added, the payload will also execute when accessing the "/apps" path.

- on "Alert Rules" section:
![Screenshot from 2024-11-06 09-41-43](https://github.com/user-attachments/assets/eac5a8b7-f482-4d28-9247-889225665b27)

- on "Custom OID" section:
![Screenshot from 2024-11-06 09-41-52](https://github.com/user-attachments/assets/1bf5525a-1b50-4262-bdc1-df27d539e766)

- on the "/apps" path:
![Screenshot from 2024-11-06 09-42-05](https://github.com/user-attachments/assets/4bd39e1e-6c60-4cc5-b922-8db7fc8094fc)



**Impact:**

Execution of Malicious Code

