# Setting User Privilege


MediaTek Cloud Sandbox(MCS) allows you to configure user access privileges for your prototypes and test devices. The settings are in the **User Privileges** tab in the **Prototype** or **device** detail pages.


MCS provides three roles:

1. The **Owner**, with access privileges to add, update, read, and delete a prototype, test device, or released device.
2. The **Administrator**, with access privilege to add, update, and read a prototype or test device.
2. The **Viewer**, with access privileges to view only a prototype or test device.


## Prototype and Device

As a prototype or device owner, or an administrator, you can add registered MCS users to access the prototype or the test device by clicking on the **User Privileges** tab in the **Prototype** or **Device** detail pages.

![](../images/User_privileges/img_privileges_01.png)


Click **Add user** to add registered MCS user to access the prototype.

![](../images/User_privileges/img_privileges_02.png)

Enter the user's email, select the roles as an administrator or a viewer, and then click **Save**.


Please note that the test device will not inherit the user privilege settings from its parent prototype. Only the owner or the administrator of the prototype can create a test device for the prototype. The test device owner is the user who created the test device. The test device owner can then modify the user privileges of the test device separately from the parent prototype.

## Beta-release and Management

MCS locks the user role to the **Prototype owner** for the beta-release of the prototype. After beta-release, only the prototype owner can create device with serial number, view and manage the released devices in the **Management** page.

A prototype's administrator and viewers cannot issue a beta-release of the prototype nor create a device for it. However, the prototype administrator can create test devices for the beta-released prototype.

