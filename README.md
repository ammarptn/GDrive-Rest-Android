# GDrive-Rest-Android
This is the library for integrate Google Drive Rest into your Android app

## Installation


Add it in your root build.gradle at the end of repositories:

	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
Step 2. Add the dependency

	dependencies {
            // Google Drive Rest library
	        implementation 'com.github.ammarptn:GDrive-Rest-Android:1.4.3'
            // For Google login
            implementation 'com.google.android.gms:play-services-auth:17.0.0'
	}
	
Step 3. Add OAuth 2.0 client IDs at [Google API console](https://console.cloud.google.com/apis)

Step 4. Enable Google Drive API in [Google API console](https://console.cloud.google.com/apis)

Step 5. Add "../auth/drive" in Scopes for Google APIs 

Optional 
Step 6. Add "../auth/drive.appdata" in Scopes if you want to access application data folder




## Usage

### Initialization


```java

	

 	GoogleSignInAccount account = GoogleSignIn.getLastSignedInAccount(getApplicationContext());
	...
	
	//if you want to use your common space of G drive
	mDriveServiceHelper = new DriveServiceHelper(getGoogleDriveService(getApplicationContext(), account, "your_app_name_here"));
	
        
```
The rest of authentication's example locate at 
https://github.com/ammarptn/GDrive-Rest-Android/blob/master/app/src/main/java/com/ammarptn/gdriverest/MainActivity.java
### Create Folder
```java
		mDriveServiceHelper.createFolder("folderName", null)
                        .addOnSuccessListener(new OnSuccessListener<GoogleDriveFileHolder>() {
                            @Override
                            public void onSuccess(GoogleDriveFileHolder googleDriveFileHolder) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolder));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());

                            }
                        });
```

### Create Text File
```java
mDriveServiceHelper.createTextFile("textFileName.txt", "some text", null)
                        .addOnSuccessListener(new OnSuccessListener<GoogleDriveFileHolder>() {
                            @Override
                            public void onSuccess(GoogleDriveFileHolder googleDriveFileHolder) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolder));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());
                            }
                        });
```

### Create Folder If Not Exist
```java
mDriveServiceHelper.createFolderIfNotExist("folderName", null)
                        .addOnSuccessListener(new OnSuccessListener<GoogleDriveFileHolder>() {
                            @Override
                            public void onSuccess(GoogleDriveFileHolder googleDriveFileHolder) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolder));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());

                            }
                        });
```

### Create Text File If Not Exist 
```java
mDriveServiceHelper.createTextFileIfNotExist("textFileName.txt","content", null)
                        .addOnSuccessListener(new OnSuccessListener<GoogleDriveFileHolder>() {
                            @Override
                            public void onSuccess(GoogleDriveFileHolder googleDriveFileHolder) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolder));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());

                            }
                        });
```

* the search result will return only file that you create from this app unless app already reviewed.

### Search File
```java
mDriveServiceHelper.searchFile("textFileName.txt", "text/plain")
                        .addOnSuccessListener(new OnSuccessListener<List<GoogleDriveFileHolder>>() {
                            @Override
                            public void onSuccess(List<GoogleDriveFileHolder> googleDriveFileHolders) {

                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolders));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());
                            }
                        });
```

### Search Folder
```java
mDriveServiceHelper.searchFolder("folderName")
                        .addOnSuccessListener(new OnSuccessListener<List<GoogleDriveFileHolder>>() {
                            @Override
                            public void onSuccess(List<GoogleDriveFileHolder> googleDriveFileHolders) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolders));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());
                            }
                        });
```
### List File/Folder in Folder
list File/Folder in Root of G-Drive, pass null as parameter
```java
mDriveServiceHelper.queryFiles(null)
                        .addOnSuccessListener(new OnSuccessListener<List<GoogleDriveFileHolder>>() {
                            @Override
                            public void onSuccess(List<GoogleDriveFileHolder> googleDriveFileHolders) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolders));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {

                            }
                        });
```

list File/Folder in specific  folder, pass folder id as parameter
```java
mDriveServiceHelper.queryFiles("g-drive-folder-id-here")
                        .addOnSuccessListener(new OnSuccessListener<List<GoogleDriveFileHolder>>() {
                            @Override
                            public void onSuccess(List<GoogleDriveFileHolder> googleDriveFileHolders) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolders));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {

                            }
                        });
```
### Upload File
```java
mDriveServiceHelper.uploadFile(new java.io.File(getApplicationContext().getFilesDir(), "fileName.txt"), "text/plain", null)
                        .addOnSuccessListener(new OnSuccessListener<GoogleDriveFileHolder>() {
                            @Override
                            public void onSuccess(GoogleDriveFileHolder googleDriveFileHolder) {
                                Gson gson = new Gson();
                                Log.d(TAG, "onSuccess: " + gson.toJson(googleDriveFileHolder));
                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Log.d(TAG, "onFailure: " + e.getMessage());
                            }
                        });
```

### Download File
```java
 mDriveServiceHelper.downloadFile(new java.io.File(getApplicationContext().getFilesDir(), "filename.txt"), "google_drive_file_id_here")
                        .addOnSuccessListener(new OnSuccessListener<Void>() {
                            @Override
                            public void onSuccess(Void aVoid) {

                            }
                        })
                        .addOnFailureListener(new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {

                            }
                        });
```

### Delete File
```java
mDriveServiceHelper.deleteFolderFile("GoogleFileId").addOnSuccessListener(new OnSuccessListener<Void>() {
                    @Override
                    public void onSuccess(Void aVoid) {
                        
                    }
                }).addOnFailureListener(new OnFailureListener() {
                    @Override
                    public void onFailure(@NonNull Exception e) {
                        
                    }
                });
```

### MimeType
```java
    public static String TYPE_AUDIO = "application/vnd.google-apps.audio";
    public static String TYPE_GOOGLE_DOCS = "application/vnd.google-apps.document";
    public static String TYPE_GOOGLE_DRAWING = "application/vnd.google-apps.drawing";
    public static String TYPE_GOOGLE_DRIVE_FILE = "application/vnd.google-apps.file";
    public static String TYPE_GOOGLE_DRIVE_FOLDER = DriveFolder.MIME_TYPE;
    public static String TYPE_GOOGLE_FORMS = "application/vnd.google-apps.form";
    public static String TYPE_GOOGLE_FUSION_TABLES = "application/vnd.google-apps.fusiontable";
    public static String TYPE_GOOGLE_MY_MAPS = "application/vnd.google-apps.map";
    public static String TYPE_PHOTO = "application/vnd.google-apps.photo";
    public static String TYPE_GOOGLE_SLIDES = "application/vnd.google-apps.presentation";
    public static String TYPE_GOOGLE_APPS_SCRIPTS = "application/vnd.google-apps.script";
    public static String TYPE_GOOGLE_SITES = "application/vnd.google-apps.site";
    public static String TYPE_GOOGLE_SHEETS = "application/vnd.google-apps.spreadsheet";
    public static String TYPE_UNKNOWN = "application/vnd.google-apps.unknown";
    public static String TYPE_VIDEO = "application/vnd.google-apps.video";
    public static String TYPE_3_RD_PARTY_SHORTCUT = "application/vnd.google-apps.drive-sdk";
```

You can use other standard MimeType as well. 
Ex. applicaiton/zip , text/plain

### Chain action
You can chain the command together. For Example, Search and delete first file that show in the result
```java
mDriveServiceHelper.searchFile("filename.txt","text/plain")
                .continueWithTask(new Continuation<List<GoogleDriveFileHolder>, Task<Void>>() {
                    @Override
                    public Task<Void> then(@NonNull Task<List<GoogleDriveFileHolder>> task) throws Exception {
                        return mDriveServiceHelper.deleteFolderFile(task.getResult().get(0).getId());
                    }
                });
```
		
more info at [Task API](https://developers.google.com/android/guides/tasks)



