# Stored-XSS-LibreNMS-Display-Name

**Description:**


XSS on the parameters (Replace $DEVICE_ID with your specific $DEVICE_ID value):`/device/$DEVICE_ID/edit` -> param: display


of Librenms versions 24.9.0 and 24.10.0 ([https://github.com/librenms/librenms](https://github.com/librenms/librenms)) allows remote attackers to inject malicious scripts. When a user views or interacts with the page displaying the data, the malicious script executes immediately, leading to potential unauthorized actions or data exposure.


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

**Additional PoC:**
1. In the "Display Name" field, enter the following payload: `"><img src onerror="alert(1)">`.
![386126249-addb1b00-23b1-4c26-8ac7-494cb24ebe8a](https://github.com/user-attachments/assets/010f7b6b-b323-4702-9af5-472984ef74d8)


2. The XSS vulnerability is triggered when accessing the "/ports" path, and the payload executes when hovering over the modified value in the "Port" field.
![386126777-446e0d62-2016-4435-a1eb-fe85079498e4](https://github.com/user-attachments/assets/b5073d2a-8b57-4ed8-a63b-94cb03f11613)


**Impact:**

Execution of Malicious Code

