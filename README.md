# QuestMediaProjection OpenXR Sample  

This repository provides an OpenXR-compatible sample for using [QuestMediaProjection](https://github.com/t34400/QuestMediaProjection) with Meta Quest. The standard setup for QuestMediaProjection using the Meta SDK does not work directly with OpenXR, so additional steps are required. This guide outlines the necessary modifications.  

## Installation  

Follow the setup steps in the **QuestMediaProjection** repository for the **Meta SDK version**, but apply the following changes:  

### **Modification to Step 1: Scene Setup**  

Instead of using the Meta SDK scene setup, perform the following steps:  

1. **Change the platform to Android**  
   - Open the menu: **File > Build Settings (Build Profiles)**  
   - Select the **Android** tab and click **Switch Platform**  

2. **Install required packages**  
   - Open **Window > Package Manager**  
   - Select **Unity Registry**  
   - Search for **Unity OpenXR Meta** and install it  

3. **Set up the AR Foundation scene**  
   - Follow the official guide: [Scene Setup](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.0/manual/project-setup/scene-setup.html)  

4. **Configure Unity OpenXR Meta**  
   - Follow the official guide: [Project Setup](https://docs.unity3d.com/Packages/com.unity.xr.meta-openxr@1.0/manual/project-setup.html)  
   - **If using passthrough**, disable **HDR Rendering** on the main camera  

### **Modification to Step 4: Editing AndroidManifest.xml**  

In addition to adding the **service** tag to the `<application>` section, you must also add the following `<meta-data>` tag:  

```xml
<application ...>
   <service
       android:name="com.t34400.mediaprojectionlib.core.MediaProjectionService"
       android:foregroundServiceType="mediaProjection"
       android:stopWithTask="true"
       android:exported="false" />
    <meta-data
        android:name="com.samsung.android.vr.application.mode"
        android:value="vr_only"/>
   ...
</application>
```  

These modifications ensure compatibility with OpenXR while enabling MediaProjection on Meta Quest.  