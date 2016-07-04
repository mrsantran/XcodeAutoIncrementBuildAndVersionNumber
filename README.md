# XcodeAutoIncrementBuildAndVersionNumber
Xcode Auto-increment Build &amp; Version Numbers

##1. Edit Scheme
![](/Screenshot/0.png)

##2. Expand "Build" section by clicking disclosure triangle and select "Pre-actions"
![](/Screenshot/2.png)

##3. Add "New Run-Script Action"
![](/Screenshot/3.png)

##4. Select "Provide build settings from $YOUR_PROJECT" and add increment script

#### Auto increment build number

```
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "${PROJECT_DIR}/${INFOPLIST_FILE}")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "${PROJECT_DIR}/${INFOPLIST_FILE}"
```

#### Auto increment version number

```
VERSIONNUM=$(/usr/libexec/PlistBuddy -c "Print CFBundleShortVersionString" "${PROJECT_DIR}/${INFOPLIST_FILE}")
NEWSUBVERSION=`echo $VERSIONNUM | awk -F "." '{print $3}'`
NEWSUBVERSION=$(($NEWSUBVERSION + 1))
NEWVERSIONSTRING=`echo $VERSIONNUM | awk -F "." '{print $1 "." $2 ".'$NEWSUBVERSION'" }'`
/usr/libexec/PlistBuddy -c "Set :CFBundleShortVersionString $NEWVERSIONSTRING" "${PROJECT_DIR}/${INFOPLIST_FILE}"
```

![](/Screenshot/4.png)
![](/Screenshot/5.png)

## 5. To test either it's work or not, you can do same thing for Debug
