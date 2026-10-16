<!-- pre-align:aligned sig=0b6ed03a5615 -->

<a id="content-delivery-image-manager-console-user-guide"></a>
## Content Delivery > Image Manager > Console User Guide { #content-delivery-image-manager-console-user-guide }

This document explains how to create folders, upload files, and manage thumbnail options using the console.

<a id="manage-folders-and-image-files"></a>
## Manage Folders and Image Files { #manage-folders-and-image-files }

You can manage folders, original image files, and created thumbnail image files on the **File View** screen of the menu.

![image_01_20220929](https://static.toastoven.net/prod_img/image_01_20220929.png)

<a id="toolbar-icon-description"></a>
### Toolbar Icon Description { #toolbar-icon-description }

![image_02_20220929](https://static.toastoven.net/prod_img/image_02_20220929.png)

<a id="create-a-folder"></a>
### Create a Folder { #create-a-folder }

![image_03_20220929](https://static.toastoven.net/prod_img/image_03_20220929.png)

1. A folder is the basic unit for storing images, and it is created by clicking the **Create Folder** button.

2. Enter a folder name and click **OK**.

   - A function to edit the name of a folder is not provided.
   - If you need to modify the name, you must delete the folder and re-create a folder.

<a id="upload-image-files"></a>
### Upload Image Files { #upload-image-files }

![image_04_20220929](https://static.toastoven.net/prod_img/image_04_20220929.png)

1. Select the desired folder to move into it, and click the **Upload** button.

   - You can upload multiple images at once, and you can also upload folders and compressed files.
   - When uploading a compressed file, the name of the folder within the compressed file must be at least two letters long.

2. Drag and drop image files, or click **Add Files** to select files to upload.

3. Select 'Overwrite' or 'Change Name' to handle files with the same name, and click **Upload**.

   - When the upload is completed normally, the screen is updated and you can check the file list.

<a id="download"></a>
### Download { #download }

![image_05_20220929](https://static.toastoven.net/prod_img/image_05_20220929.png)

1. After selecting a folder or image files to download, click the **Download** button.

2. If you select one image file after clicking the **OK** button, it will be downloaded immediately. If you select two or more files, the compressed file `nhn_cloud_image_manager.zip` will be downloaded.

   - You can only download up to 10,000 images at a time, and even if you download images stored in a folder, only 10,000 images can be downloaded in the same way.

<a id="delete-files-or-a-folder"></a>
### Delete Files or a Folder { #delete-files-or-a-folder }

![image_06_20220929](https://static.toastoven.net/prod_img/image_06_20220929.png)

1. After selecting the folder or image files to delete, click the **Delete** button.

2. Click **Confirm**.

   - If you select a folder, all files in that folder are also deleted.

<a id="view-properties"></a>
### View Properties { #view-properties }

![image_07_20231031](https://static.toastoven.net/prod_img/image_07_20231031.png)

Select one folder or image file and click the **Properties** button.

- If you select an image file, you can check the image's width and height, download URL, and meta information.

<a id="query-and-view-the-list"></a>
### Query and View the List { #query-and-view-the-list }

![image_08_20220929](https://static.toastoven.net/prod_img/image_08_20220929.png)

1. You can view files after filtering by the type of image file using 'View Filter'.

   - 'Original Image' means an image file uploaded directly through the console or API, and 'Created Thumbnail' means an image created by applying an operation to the original image.

2. Search for the image file name from the current location or from the entire location.

   - All results that contain a search term are retrieved, similar to `like '%search term%'` in the database.
   - Searches are case-sensitive.
      - Input example: sample
      - Example results: sample.gif, sample_2.gif, sample 3.gif, sample_sample_100x100.png

<a id="delete-all-files"></a>
### Delete All Files { #delete-all-files }

![image_09_20220929](https://static.toastoven.net/prod_img/image_09_20220929.png)

1. Click **Delete All Files**.

   - To terminate the use of the service, all files must be deleted.
   - A deleted file cannot be recovered, so use it with caution.

2. Click **Confirm**.

<a id="manage-thumbnail-options"></a>
## Manage Thumbnail Options { #manage-thumbnail-options }

![image_10_20220929](https://static.toastoven.net/prod_img/image_10_20220929.png)

Thumbnail options can be managed from the **Settings** screen of the menu.

You can generate thumbnails by a combination of several options.

<a id="create-thumbnails"></a>
### Create Thumbnails { #create-thumbnails }

![image_11_20220929](https://static.toastoven.net/prod_img/image_11_20220929.png)

1. Click **Add** to add thumbnail options.

2. Set name and description

   - Enter a name and description.
   - When there is the same option name, it is recommended to add a identifier after it.
   - For the description, enter a brief description of the thumbnail option for easy identification by users.

3. Set image processing options

   - Set image processing options.
   - Select the image generation quality and format.
   - In 'Callback URL', enter the address to be notified of the thumbnail generation result.
   - Select or clear the options 'Enable Real-time Processing', 'Maintain Image Meta Information', 'Rotate by Orientation', and 'Maintain GIF Animation'.
   - Circle Crop and Watermark, which are image composition, do not maintain the GIF animation effect.

4. Add image operation scenario

   - Click **+Add** to select image operation options.
   - Scenarios are run by group and the same option cannot be configured in duplicate.
   - Within the group, click the arrow button (▲▼) on the right side to set the scenario order.

![image_12_20220929](https://static.toastoven.net/prod_img/image_12_20220929.png)

The resizing of thumbnails are performed as follows.

- Change the size based on the longer side of Option: Perform resize while maintaining the ratio.
   - Example: If you resize a 400x300 image with the thumbnail size option 200x100, it will be resized to a 200x150 image.
- Change the size based on the shorter side of Option: Perform resize while maintaining the ratio.
   - Example: If you resize a 400x300 image with the thumbnail size option 200x100, it will be resized to a 133x100 image.
- Change the size to fit the width and height of Option: Perform resize to the configured size without maintaining the ratio.
   - Example: If you resize a 400x300 image with the thumbnail size option 200x100, it will be resized to a 200x100 image.
- Change the size based on the width of Option: Perform resize while maintaining the ratio.
   - Example: If you resize a 400x300 image with the thumbnail size option 200x100, it will be resized to a 200x150 image.
- Change the size based on the height of Option: Perform resize while maintaining the proportions.
   - Example: If you resize a 400x300 image with the thumbnail size option 200x100, it will be resized to a 133x100 image.

After completing the scenario settings, click **Save**.

<a id="edit-thumbnails"></a>
### Edit Thumbnails { #edit-thumbnails }

![image_13_20220929](https://static.toastoven.net/prod_img/image_13_20220929.png)

1. Select a thumbnail and click **Edit**.

2. Edit the thumbnail options and click **Edit**.

   - Even if you modify the options, the thumbnails created with the settings before modification are not modified.
   - If you check the 'Delete Operation Image' checkbox in the dialog box, you can bulk delete thumbnails created with the settings before modification.

<a id="delete-thumbnails"></a>
### Delete Thumbnails { #delete-thumbnails }

![image_14_20220929](https://static.toastoven.net/prod_img/image_14_20220929.png)

Click **Delete** to delete the thumbnail option.

- You can delete the selected thumbnail option with the Delete button.
- If you check the 'Delete Operation Image' checkbox in the dialog box, you can bulk delete thumbnails created with the operation.

<a id="user-settings"></a>
### User Settings { #user-settings }

![image_15_20220929](https://static.toastoven.net/prod_img/image_15_20220929.png)

1. Click **Setting**.

2. Choose to enable/disable real-time processing.
