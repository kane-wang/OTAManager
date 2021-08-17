# OTAManager

downloadApplyABOTA
public void downloadApplyABOTA(Context context,
                               java.lang.String accessToken,
                               java.lang.String otaURL,
                               java.lang.String otaPath,
                               java.lang.String otaVersion,
                               Handler handler)
This method is used to download OTA file from remote http server or from local file path, VERIFY the OTA file and APPLY the update. A token is required prior to calling this function.
1. otaURL will get first precedence. To ignore the otaURL argument an empty string can be provided. An online token is required to download OTA from otaURL.
2. otaVersion will get second precedence. Ota versions can be procured by calling getAvailableVersions(). To ignore this argument, an empty string can be provided. An online token is required to download OTA by specifying version.
3. otaUri (local file path) will get next precedence. Download from local path can be done without an online token.
4. Fourth precedence falls to the elo default upgrade server. This is used if empty strings are provided for otaURL and otaVersion. This requires an online token.

The OS upgrade files are downloaded using the Android Update Engine. Failures are possible; for example when an incorrect status, download URL, or a nonexistent version number is provided, the download manager will show STATUS_FAILED in logcat. More information on the behavior of the Android download manager and its constant values can be found at: https://developer.android.com/reference/android/app/DownloadManager.
Each time you trigger an OTA download using the API, the ota directory will be cleared. When the verify and apply APIs are used, the last download that was completed will be used.
Before starting the download, this method will check if a previously downloaded OTA package exists. If it does, the package will be extracted and the version will be checked against the latest available version to see if avoiding the download is possible. If the existing OTA package cannot be read, the old package will be removed and a new download of the latest OTA package will be started.

Parameters:
context - A context object of the calling Class (Activity/Service).
accessToken - An authentication token received from the Elo servers.
otaURL - A custom download URL can be provided, or an empty string can be passed to use default URL.
otaPath - A custom OTA path on the device (eg. /sdcard/Download/ota.zip)
otaVersion - A custom OTA package version can be provided (eg. 5.5.11+p)
handler - A handler to receive one or more of the following callback messages:
AccountManager.TOKEN_VERIFY_FAIL
OTA_DOWNLOAD_REMOTE_FILE_PERCENTAGE
OTA_APPLY_IN_PROGRESS
Consts.GENERIC_ERROR
