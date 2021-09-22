# misc-exiftool-tricks

## Extract GPS location data from FILE:
```powershell
exiftool -GPSPosition FILE
```

## List all editable time-related fields of FILE:
```powershell
exiftool -a -s -G1 -time:all FILE
```

## Set EXIF and creation/modification date from the filename:
```powershell
exiftool "-datetime<filename" "-datetimeoriginal<filename" "-FileModifyDate<filename" "-FileCreateDate<filename" .
```

## Set creation/modification date from EXIF:
```powershell
exiftool "-FileModifyDate<DateTimeOriginal" "-FileCreateDate<DateTimeOriginal" "-DateTime<DateTimeOriginal" .
```

## Set EXIF and creation date based on the modification date:
```powershell
exiftool -P "-DateTime<FileModifyDate" "-DateTimeOriginal<FileModifyDate" "-FileCreateDate<FileModifyDate" .
```

## Set modification date from the filename that contains a UNIX epoch (NOTE: uses UTC, not CET!)
```powershell
exiftool  "-filemodifydate<${filename;/(\d{10})/ and $_ = $1}" -d %s .
```

## Shift all EXIF dates FORWARD (hence the +) by YY:MM:DD hh:mm:ss:
```powershell
exiftool "-AllDates+=YY:MM:DD hh:mm:ss" .
```

## Set EXIF dates of MP4 videos from modification date (sometimes -CreateDate is the flag):
```powershell
exiftool "-MediaCreateDate=FileModifyDate" -P .
```

## Set EXIF dates of MP4 videos from filename:
```powershell
exiftool "-MediaCreateDate<FileName" "-FileModifyDate<FileName" -P .
```
