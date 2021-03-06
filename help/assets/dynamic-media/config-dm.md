---
title: Configuring Dynamic Media Cloud Service
description: Information on how to configure Dynamic Media in Adobe Experience Manager Cloud Service.
---

# About configuring Dynamic Media Cloud Service {#configuring-dynamic-media-scene-mode}

If you use Adobe Experience Manager set up for different environments, such as one for development, one for staging, and one for live production, you need to configure Dynamic Media Cloud Services for each one of those environments.

## Architecture diagram of Dynamic Media {#architecture-diagram-of-dynamic-media-scene-mode}

The following architecture diagram describes how Dynamic Media works.

With the new architecture, AEM is responsible for primary source assets and synchs with Dynamic Media for asset processing and publishing:

1. When the primary source asset is uploaded to AEM, it is replicated to Dynamic Media. At that point, Dynamic Media handles all asset processing and rendition generation, such as video encoding and dynamic variants of an image.
1. After the renditions are generated, AEM can securely access and preview the remote Dynamic Media renditions (no binaries are sent back to the AEM instance).
1. After content is ready to be published and approved, it triggers the Dynamic Media service to push content out to delivery servers and cache content at the CDN.

![chlimage_1-550](assets/chlimage_1-550.png)

<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading AEM Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your AEM instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Creating a new Dynamic Media Configuration in Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must [log in](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) to Dynamic Media Classic to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In AEM, tap the AEM logo to access the global navigation console.
1. On the left side of the console, tap the Tools icon, then tap **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. On the Dynamic Media Configuration Browser page, in the left pane, tap **[!UICONTROL global]** (do not tap or select the folder icon to the left of **[!UICONTROL global]**), then tap **[!UICONTROL Create]**.
1. On the **[!UICONTROL Create Dynamic Media Configuration]** page, enter a title, the Dynamic Media account email address, password, then select your region. These are provided to you by Adobe in the provisioning email. Please contact support if you did not receive this.
1. Click **[!UICONTROL Connect to Dynamic Media]**.
1. In the **[!UICONTROL Change Password]** dialog box, in the **[!UICONTROL New Password]** field, enter a new password that consists of 8-25 characters. The password must contain at least one of each of the following:

      * Uppercase letter
      * Lowercase letter
      * Number
      * Special character: `# $ & . - _ : { }`

      Note that the **[!UICONTROL Current Password]** field is intentionally pre-filled and hidden from interaction. 

      If necessary, you can check the spelling of a password you have typed or retyped by tapping the password eye icon to reveal the password. Tap the icon again to hide the password.

1. In the **[!UICONTROL Repeat Password]** field, retype the new password, then tap **[!UICONTROL Done.]** 

   The new password is saved when you tap **[!UICONTROL Save]** in the upper-right corner of the **[!UICONTROL Create Dynamic Media Configuration]** page.

   If you tapped **[!UICONTROL Cancel]** in the **[!UICONTROL Change Password]** dialog box, you are still required to enter a new password when you tap **[!UICONTROL Save]** to save the newly created Dynamic Media configuration.
  
   See also [Changing the password to Dynamic Media](#change-dm-password).

1. When the connection is successful, you can set the following:

   | Property | Description |
   |---|---|
   | Company | The name of the Dynamic Media account. It is possible you may have multiple Dynamic Media accounts for different sub-brands, divisions, or different staging/production environments. |
   | Company Root Folder Path | Your company's root folder path. |
   | Publishing Assets | You can choose from the following three options:<br>**[!UICONTROL Immediately]**: When assets are uploaded, the system ingests the assets and provides the URL/Embed instantly. There is no user intervention necessary to publish assets.<br>**[!UICONTROL Upon Activation]**: You need to explicitly publish the asset first before a URL/Embed link is provided.<br>**[!UICONTROL Selective Publish]**: Assets are auto published for secure preview only and can be explicitly published to AEM without publishing to DMS7 for delivery in the public domain. In the future, Adobe will enhance this option to publish assets to AEM and publish assets to Dynamic Media, mutually exclusive of each other. That is, you can publish assets to DMS7 so you can use features such a Smart Crop or dynamic renditions. Or, you can publish assets exclusively in AEM for previewing; those same assets are not published in DMS7 for delivery in the public domain. |
   | Secure Preview Server | Lets you specify the URL path to your secure renditions preview server. That is, after renditions are generated, AEM can securely access and preview the remote Dynamic Media renditions (no binaries are sent back to the AEM instance).<br>Unless you have a special arrangment to use your own company's server or a special server, Adobe Systems recommends that you leave this setting as specified. |
   | Sync all content | Selected by default. Deselect this option if you want to selectively include or exclude assets from the sync to Dynamic Media. Deselecting this option lets you can choose from the following two Dynamic Media sync modes:<br>**[!UICONTROL Dynamic Media sync mode]**<br>**[!UICONTROL Enable by default]**: The configuration is applied to all folders by default unless you mark a folder specifically for exclusion. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabled by default]**: The configuration is not applied to any folder until you explicitly mark a selected folder for sync to Dynamic Media.<br>To mark a selected folder for sync to Dynamic Media, select an asset folder, then on the toolbar, tap **[!UICONTROL Properties]**. On the **[!UICONTROL Details]** tab, in the **[!UICONTROL Dynamic Media sync mode]** drop-down list, choose from the following three options. When you are done, tap **[!UICONTROL Save]**. *Remember: these three options are not available if you selected **Sync all content** earlier.* See also [Working with Selective Publish at the folder level in Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)<br>**[!UICONTROL Inherited]**: No explicit sync value on the folder; instead, the folder inherits the sync value from one of its ancestor folders or the default mode in the cloud configuration. The detailed status for inherited shows by way of a tool tip.<br>**[!UICONTROL Enable for sub-folders]**: Include everything in this sub-tree for sync to Dynamic Media. The folder-specific settings override the default mode in the cloud configuration.<br>**[!UICONTROL Disabled for sub-folders]**: Exclude everything in this sub-tree from syncing to Dynamic Media. |

   >[!NOTE]
   >
   >There is no support for versioning in Dynamic Media. Also, delayed activation applies only if **[!UICONTROL Publish Assets]** in the Edit Dynamic Media Configuration page is set to **[!UICONTROL Upon Activation]**, and then only until the first time the asset is activated.
   >
   >
   >After an asset is activated, any updates are immediately published live to S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Tap **[!UICONTROL Save]**. The new Dynamic Media password and configuration is saved. If you tapped **[!UICONTROL Cancel]** instead, no password update occurs.
1. In the **[!UICONTROL Configuring Dynamic Media]** dialog box, tap **[!UICONTROL OK]** to begin the configuration.

   >[!IMPORTANT]
   >
   >When the new Dynamic Media configuration finishes its setup, you will receive a status notification within AEM's Inbox.
   >
   >This Inbox notification informs you if the configuration was either successful or not.
   > See [Troubleshooting a new Dynamic Media configuration](#troubleshoot-dm-config) and [Your Inbox](/help/sites-cloud/authoring/getting-started/inbox.md) for more information. 

1. To securely preview Dynamic Media content before it gets published, you need to "allowlist" the AEM author instance to connect to Dynamic Media. To set this up, do the following:

    * Log on to your Dynamic Media Classic account: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html). Your credentials and logon were provided by Adobe at the time of provisioning. If you do not have this information, contact Technical Support.
    * On the navigation bar near the top right of the page, click **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.

    * On the Image Server Publish page, in the Publish Context drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, tap **[!UICONTROL Add]**.
    * Select the check box to enable (turn on) the address, and then enter the IP address of the AEM Author instance (not Dispatcher IP).
    * Click **[!UICONTROL Save]**.

You are now finished with the basic configuration; you are ready to use Dynamic Media.

If you want to further customize your configuration, you can optionally complete any of the tasks under [Configuring Advanced Settings in Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Troubleshooting a new Dynamic Media Configuration {#troubleshoot-dm-config}

When a new Dynamic Media configuration finishes its setup, you will receive a status notification within AEM's Inbox. This notification informs you if the configuration was either successful or not, as seen in the following respective images from the Inbox.

   ![aeminboxsuccess](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

   ![aeminboxfailure](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

See also [Your Inbox](/help/sites-cloud/authoring/getting-started/inbox.md).

**To troubleshoot a new Dynamic Media configuration**

1. Near the upper-right corner of the AEM page, tap the bell icon, then tap **[!UICONTROL View All]**.
1. On the Inbox page, tap the success notification to read an overview of the status and logs of the configuration.

   If the configuration failed, tap the failure notification similar to the following screenshot.

   ![dmsetupfailed](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. On the **[!UICONTROL DMSETUP]** page, review the configuration details that describe the failure. In particular, take note of any error messages or error codes. You will need to contact Adobe Care with this information.

   ![dmsetuppage](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Changing the password to Dynamic Media {#change-dm-password}

Password expiration in Dynamic Media is set to 100 years from the current system date.

The password must contain at least one of each of the following:

* Uppercase letter
* Lowercase letter
* Number
* Special character: `# $ & . - _ : { }`

If necessary, you can check the spelling of a password you have typed or retyped by tapping the password eye icon to reveal the password. Tap the icon again to hide the password.

The changed password is saved when you tap **[!UICONTROL Save]** in the upper-right corner of the **[!UICONTROL Edit Dynamic Media Configuration]** page.

1. In AEM, tap the AEM logo to access the global navigation console.
1. On the left side of the console, tap the Tools icon, then tap **[!UICONTROL Cloud Services > Dynamic Media Configuration.]**
1. On the Dynamic Media Configuration Browser page, in the left pane, tap **[!UICONTROL global]** (do not tap or select the folder icon to the left of **[!UICONTROL global]**), then tap **[!UICONTROL Edit.]**
1. On the **[!UICONTROL Edit Dynamic Media Configuration]** page, directly below the **[!UICONTROL Password]** field, tap **[!UICONTROL Change Password.]**
1. In the **[!UICONTROL Change Password]** dialog box, do the following:

   * In the **[!UICONTROL New Password]** field, enter a new password.

      Note that the **[!UICONTROL Current Password]** field is intentionally pre-filled and hidden from interaction.

   * In the **[!UICONTROL Repeat Password]** field, retype the new password, then tap **[!UICONTROL Done.]**

1. In the upper-right corner of the **[!UICONTROL Edit Dynamic Media Configuration]** page, tap **[!UICONTROL Save]**, then tap **[!UICONTROL OK.]**

## (Optional) Configuring Advanced Settings in Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

If you want to further customize the configuration and setup of Dynamic Media, or optimize its performance, you can complete one or more of the following *optional* tasks:

* [Setup and configuration of Dynamic Media settings](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Optional) Tuning the performance of Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Optional) Setup and configuration of Dynamic Media settings {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Use the Dynamic Media Classic (Scene7) user interface to make changes to your Dynamic Media settings.

Some of the tasks above require that you log into Dynamic Media Classic (Scene7) here: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

Setup and configuration tasks include the following:

* [Publishing setup for Image Server](#publishing-setup-for-image-server)
* [Configuring application general settings](#configuring-application-general-settings)
* [Configuring color management](#configuring-color-management)
* [Editing MIME types for supported formats](#editing-mime-types-for-supported-formats)
* [Adding MIME types for unsupported formats](#adding-mime-types-for-unsupported-formats)
<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Publishing setup for Image Server {#publishing-setup-for-image-server}

The Publish Setup settings determine how assets are delivered by default from Dynamic Media. If no setting is specified, Dynamic Media delivers an asset according to the default settings defined in Publish Setup. For example, a request to deliver an image that does not include a resolution attribute yields an image with the Default Object Resolution setting.

To configure Publish Setup: in Dynamic Media Classic, click **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.

The Image Server screen establishes default settings for delivering images. See the UI screen for description of each setting.

**[!UICONTROL Request Attributes]** - These settings impose limits on images that can be delivered from the server.
**[!UICONTROL Default Request Attributes]** - These settings pertain to the default appearance of images.
**[!UICONTROL Common Thumbnail Attributes]** - These settings pertain to the default appearance of thumbnail images.
**[!UICONTROL Defaults for Catalog Fields]**- These settings pertain to the resolution and default thumbnail type of images.
**[!UICONTROL Color Management Attributes]** - These settings determine which ICC color profiles are used.
**[!UICONTROL Compatibility Attributes]** - This setting enables leading and trailing paragraphs in text layers to be treated as they were in version 3.6 for backwards compatibility.
**[!UICONTROL Localization Support]** - These settings let you manage multiple locale attributes. It also lets you specify a locale map string so you can define which languages you want to support for the various tooltips in Viewers. For more information about setting up **[!UICONTROL Localization Support]**, see [Considerations when setting up localization of assets](https://experienceleague.corp.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Configuring application general settings {#configuring-application-general-settings}

To open the Application General Settings page, in Dynamic Media Classic Global Navigation bar, click **[!UICONTROL Setup > Application Setup > General Settings.]**

**[!UICONTROL Servers]** - On account provisioning, Dynamic Media automatically provides the assigned servers for your company. These servers are used to construct URL strings for your web site and applications. These URL calls are specific to your account. Do not change any of the server names unless explicitly instructed to do so by AEM support.
**[!UICONTROL Overwrite Images]** - Dynamic Media does not allow two files to have the same name. Each item's URL ID (the filename minus the extension) must be unique. These options specify how replacement assets are uploaded: whether they replace the original or become duplicate. Duplicate assets are renamed with a “-1” (for example, chair.tif is renamed chair-1.tif). These options affect assets uploaded to a different folder than the original or assets with a different filename extension from the original (such as JPG, TIF, or PNG).
**[!UICONTROL Overwrite in current folder, same base image name/extension]** - This option is the strictest rule for replacement. It requires that you upload the replacement image to the same folder as the original, and that the replacement image has the same filename extension as the original. If these requirements are not met, a duplicate is created. To maintain consistency with AEM, always choose **[!UICONTROL Overwrite in current folder, same base image name/extension]**.
**[!UICONTROL Overwrite in any folder, same base asset name/extension]** - Requires that the replacement image has the same filename extension as the original image (for example, chair.jpg must replace chair.jpg, not chair.tif). However, you can upload the replacement image to a different folder than the original. The updated image resides in the new folder; the file can no longer be found in its original location.
**[!UICONTROL Overwrite in any folder, same base asset name regardless of extension]** - This option is the most inclusive replacement rule. You can upload a replacement image to a different folder than the original, upload a file with a different filename extension, and replace the original file. If the original file is in a different folder, the replacement image resides in the new folder to which it was uploaded.
**[!UICONTROL Default Color Profiles]** - See [Configuring Color Management](#configuring-color-management) for additional information. By default, the system shows 15 renditions when you select **[!UICONTROL Renditions]** and 15 viewer presets when you select **[!UICONTROL Viewers]** in the asset's detail view. You can increase this limit. See [Increasing or decreasing the number of image presets that display](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) or [Increasing or decreasing the number of viewer presets that display](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Configuring color management {#configuring-color-management}

Dynamic media color management lets you color correct assets. With color correction, ingested assets retain their color space (RGB, CMYK, Gray) and embedded color profile. When you request a dynamic rendition, the image color is corrected into the target color space using CMYK, RGB, or Gray output. See [Configuring Image Presets](/help/assets/dynamic-media/managing-image-presets.md).

To configure the default color properties to enable color correction when requesting images:

1. [Log into Dynamic Media Classic](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) using credentials provided during provisioning. Navigate to **[!UICONTROL Setup > Application Setup]**.
1. Expand the **[!UICONTROL Publish Setup]** area and select **[!UICONTROL Image Server]**. Set **[!UICONTROL Publish Context]** to **[!UICONTROL Image Serving]** when setting defaults for publish instances.
1. Scroll to the property you need to change, for example a property in the **[!UICONTROL Color Management Attributes]** area.
   You can set the following color correction properties:

   | Property | Description |
   |---|---|
   | CMYK Default Color Space | Name of the default CMYK color profile. |
   | Gray-Scale Default Color Space | Name of the default Gray color profile. |
   | RGB Default Color Space | Name of the default RGB color profile. |
   | Color Conversion Rendering Intent | Specifies the render intent. Acceptable values are: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric.]** Adobe recommends **[!UICONTROL relative]** as the default. |

1. Tap **[!UICONTROL Save]**.

For example, you could set the **[!UICONTROL RGB Default Color Space]** to *sRGB*, and **[!UICONTROL CMYK Default Color Space]** to *WebCoated*.

Doing so would do the following:

* Enables color correction for RGB and CMYK images.
* RGB images that do not have a color profile will be assumed to be in the *sRGB* color space.
* CMYK images that do not have a color profile will be assumed to be in *WebCoated* color space.
* Dynamic renditions that return RGB output, will return it in the *sRGB* color space.
* Dynamic renditions that return CMYK output, will return it in the *WebCoated* color space.

#### Editing MIME types for supported formats {#editing-mime-types-for-supported-formats}

You can define which asset types are processed by Dynamic Media and customize advanced asset processing parameters. For example, you can specify asset processing parameters to do the following:

* Convert an Adobe PDF to an eCatalog asset.
* Convert an Adobe Photoshop Document (.PSD) to a banner template asset for personalization.
* Rasterize an Adobe Illustrator file (.AI) or an Adobe Photoshop Encapsulated Postscript file (.EPS).
* [Video Profiles](/help/assets/dynamic-media/video-profiles.md) and [Imaging Profiles](/help/assets/dynamic-media/image-profiles.md) can be used to define processing of videos and images, respectively.

See [Uploading Assets](/help/assets/add-assets.md).

**To edit the MIME types for supported formats**

1. In AEM, click the AEM logo to access the global navigation console, then click **[!UICONTROL General > CRXDE Lite]**.
1. In the left rail, navigate to the following:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. Under the mimeTypes folder, select a mime type.
1. On the right side of the CRXDE Lite page, in the lower portion:

   * Double-click the **[!UICONTROL enabled]** field. By default all asset mime types are enabled (set to **[!UICONTROL true]**), which means the assets will be synched to Dynamic Media for processing. If you want to exclude this asset mime type from being processed, change this setting to **[!UICONTROL false]**.

   * Double-click **[!UICONTROL jobParam]** to open its associated text field. See [Supported Mime Types](/help/assets/file-format-support.md) for a list of permitted processing parameter values you can use for a given mime type.

1. Do one of the following:
   * Repeat steps 3-4 to edit additional mime types.
   * On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**

1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to AEM.

#### Adding MIME types for unsupported formats {#adding-mime-types-for-unsupported-formats}

You can add custom MIME types for unsupported formats in AEM Assets. To ensure that any new node you add in CRXDE Lite is not deleted by AEM, you must ensure that you move the MIME type before `image_` and its enabled value is set to **[!UICONTROL false]**.

**To add MIME types for unsupported formats**

1. From AEM, tap **[!UICONTROL Tools > Operations > Web Console.]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. A new browser tab opens to the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. On the page, scroll down to the name *Adobe CQ Scene7 Asset MIME type Service* as seen the following screenshot. To the right of the name, tap the **[!UICONTROL Edit the configuration values]** (pencil icon).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. On the **Adobe CQ Scene7 Asset MIME type Service** page, click any plus sign icon &lt;+&gt;. The location in the table where you click the plus sign to add the new mime type is trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Type `DWG=image/vnd.dwg` in the empty text field that you just added.

   Note that the example `DWG=image/vnd.dwg` is for illustration purposes only. The MIME type that you add here can be any other unsupported format.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. In the lower-right corner of the page, tap **[!UICONTROL Save]**.

   At this point, you can close the browser tab that has the open Adobe Experience Manager Web Console Configuration page.

1. Return to the browser tab that has your open AEM console.
1. From AEM, tap **[!UICONTROL Tools > General > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. In the left rail, navigate to the following:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Drag the mime type `image_vnd.dwg` and drop it directly above `image_` in the tree as seen in the following screenshot.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. With the mime type `image_vnd.dwg` still selected, from the **[!UICONTROL Properties]** tab, in the **[!UICONTROL enabled]** row, under the **[!UICONTROL Value]** column header, double-click the value to open the **[!UICONTROL Value]** drop-down list.
1. Type `false` in the field (or select **[!UICONTROL false]** from the drop-down list).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Near the upper-left corner of the CRXDE Lite page, click **[!UICONTROL Save All]**.



### (Optional) Tuning the performance of Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

To keep Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> running smoothly, Adobe recommends the following synchronization performance/scalability fine-tuning tips:

* Updating the predefined Job parameters for processing of different file formats.
* Updating the predefined Granite workflow (video assets) queue worker threads.
* Updating the predefined Granite transient workflow (images and non-video assets) queue worker threads.
* Updating the maximum upload connections to the Dynamic Media Classic server.

#### Updating the predefined Job parameters for processing of different file formats

You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`.

Adobe recommends using the following "tuned" job parameters for PDF, Postscript, and PSD files:

| File type | Recommended job parameters |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| Postscript | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- To update any of these parameters, follow the steps in [Enabling MIME type-based Assets/Dynamic Media Classic upload job parameter support](#enabling-mime-type-based-assets-scene-upload-job-parameter-support). -->

#### Updating the Granite Transient Workflow queue {#updating-the-granite-transient-workflow-queue}

The Granite Transit Workflow queue is used for the **[!UICONTROL DAM Update Asset]** workflow. In Dynamic Media, it is used for image ingestion and processing.

**To update the Granite Transient Workflow queue**

1. Navigate to [https://&lt;server&gt;/system/console/configMgr](https://localhost:4502/system/console/configMgr) and search for **Queue: Granite Transient Workflow Queue**.

   >[!NOTE]
   >
   >A text search is necessary instead of a direct URL because the OSGi PID is dynamically generated.

1. In the **[!UICONTROL Maximum Parallel Jobs]** field, change the number to the desired value.

   You can increase **[!UICONTROL Maximum Parallel Jobs]** to adequately support heavy upload of files to Dynamic Media. The exact value is dependent on hardware capacity. In certain scenarios&ndash;that is, an initial migration or a one-time bulk upload&ndash;you can use a large value. Be aware, however, that using a large value (such as two times the number of cores) may have negative effects on other concurrent activities. As such, you should test and adjust the value based on your particular use case.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Tap **[!UICONTROL Save]**.

#### Updating the Granite Workflow queue {#updating-the-granite-workflow-queue}

The Granite Workflow queue is used for non-transient workflows. In Dynamic Media, it used to to process video with the **[!UICONTROL Dynamic Media Encode Video]** workflow.

To update the Granite Workflow queue:

1. Navigate to `https://<server>/system/console/configMgr` and search for **Queue: Granite Workflow Queue**.

   >[!NOTE]
   >
   >A text search is necessary instead of a direct URL because the OSGi PID is dynamically generated.

1. In the **[!UICONTROL Maximum Parallel Jobs]** field, change the number to the desired value.

   By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   For most use cases, the 0.5 default setting is sufficient.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Tap **[!UICONTROL Save]**.

#### Updating the Scene7 upload connection {#updating-the-scene-upload-connection}

The Scene7 Upload Connection setting synchronizes AEM assets to Dynamic Media Classic servers.

To update the Scene7 upload connection:

1. Navigate to `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. In the **[!UICONTROL Number of connections]** field and/or the **[!UICONTROL Active job timeout]** field, change the number as desired.

   The **[!UICONTROL Number of connections]** setting controls the maximum number of HTTP connections allowed for AEM to Dynamic Media upload; typically, the predefined value of 10 connections is sufficient.

   The **[!UICONTROL Active job timeout]** setting determines the wait time for uploaded Dynamic Media assets to be published in delivery server. This value is 2100 seconds or 35 minutes by default.

   For most use cases, the setting of 2100 is sufficient.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Tap **[!UICONTROL Save.]**

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your AEM author environment to the AEM publish node. This workflow is necessary because the AEM publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to AEM publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the AEM publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the AEM publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In AEM, tap the AEM logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
   