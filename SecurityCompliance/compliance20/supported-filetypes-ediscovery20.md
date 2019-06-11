---
title: "Supported file types in Advanced eDiscovery"
ms.reviewer: 
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: ""
---

# Supported file types in Advanced eDiscovery

Advanced eDiscovery supports many file types to many different levels, which are described in the following table. This list isn't finalized, and we'll add new file types as we continue our validation testing. The tables indicates if a file type is supported for text extraction (OCR for images), viewable in the native viewer and also support in the Annotate viewer in Advanced eDiscovery.

## Archive / Container

| Mime type | File identification | Metadata extraction | Container extraction | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |
| application/x-7z-compressed | Yes | Yes | Yes | .7z |
| application/x-rar-compressed | Yes | Yes | Yes | .rar |
| application/x-tar | Yes | Yes | Yes | .tar |
| application/zip | Yes | Yes | Yes | .zip |
||||||||

## Database

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/x-msaccess | Yes | Yes | Yes | No | No | .mdb |
||||||||

## Email

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.ms-outlook | Yes | Yes | Yes | Yes | Yes | .msg |
| message/rfc822 | Yes | Yes | Yes | Yes | Yes | .eml |
| text/vcard-contact | Yes | Yes | Yes | Yes | Yes | .vcf |
||||||||

## Email Container

| Mime type | File identification | Metadata extraction | Container extraction | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |
| application/mbox | Yes | Yes | Yes | .mbox |
| application/vnd.ms-outlook-pst | Yes | Yes | Yes | .pst |
||||||||

## HTML

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/xhtml+xml | Yes | Yes | Yes | Yes | Yes | .xhtml |
| application/xml | Yes | Yes | Yes | Yes | Yes | .xml |
| text/html | Yes | Yes | Yes | Yes | Yes | .htm; .html; .shtml |
||||||||

## Image

| Mime type | File identification | Metadata extraction | OCR Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| image/bmp | Yes | Yes | Yes | Yes | Yes | .bmp |
| image/emf | Yes | Yes | Yes | Yes | Yes | .emf |
| image/gif | Yes | Yes | Yes | Yes | Yes | .gif |
| image/jpeg | Yes | Yes | Yes | Yes | Yes | .jpeg; .jpg |
| image/png | Yes | Yes | Yes | Yes | Yes | .png |
| image/svg+xml | Yes | Yes | Yes | Yes | No | .svg |
| image/tiff | Yes | Yes | Yes | Yes | Yes | .tif |
| image/vnd.dwg | Yes | Yes | Yes | Yes | Yes | .dwg; .dxf |
| image/wmf | Yes | Yes | Yes | Yes | Yes | .wmf |
||||||||

## Microsoft Excel

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.ms-excel | Yes | Yes | Yes | Yes | Yes | .dat; .xls |
| application/vnd.ms-excel.sheet.binary.macroenabled.12 | Yes | Yes | Yes | Yes | No | .xlsb |
| application/vnd.ms-excel.sheet.macroenabled.12 | Yes | Yes | Yes | Yes | Yes | .xlsm |
| application/vnd.ms-excel.template.macroenabled.12 | Yes | Yes | Yes | No | No | .xltm |
| application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | Yes | Yes | Yes | Yes | Yes | .xlsx |
| application/vnd.openxmlformats-officedocument.spreadsheetml.template | Yes | Yes | Yes | Yes | Yes | .xltx |
||||||||

## Microsoft Powerpoint

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.ms-powerpoint | Yes | Yes | Yes | Yes | Yes | .pot; .pps; .ppt |
| application/vnd.openxmlformats-officedocument.presentationml.presentation | Yes | Yes | Yes | Yes | Yes | .pptx |
| application/vnd.openxmlformats-officedocument.presentationml.slideshow | Yes | Yes | Yes | Yes | Yes | .ppsx |
| application/vnd.openxmlformats-officedocument.presentationml.template | Yes | Yes | Yes | Yes | Yes | .potx |
||||||||

## Microsoft Publisher

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/x-mspublisher | Yes | Yes | Yes | Yes | Yes | .pub |
||||||||

## Microsoft Visio

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.ms-visio.drawing | Yes | Yes | Yes | Yes | No |  |
| application/vnd.visio | Yes | Yes | Yes | Yes | Yes | .vsd |
||||||||

## Microsoft Word

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/msword | Yes | Yes | Yes | Yes | Yes | .dat; .doc |
| application/rtf | Yes | Yes | Yes | Yes | Yes | .doc; .rtf |
| application/vnd.ms-word.document.macroenabled.12 | Yes | Yes | Yes | Yes | Yes | .docm |
| application/vnd.ms-word.template.macroenabled.12 | Yes | Yes | Yes | Yes | Yes | .dotm |
| application/vnd.openxmlformats-officedocument.wordprocessingml.document | Yes | Yes | Yes | Yes | Yes | .docx |
| application/vnd.openxmlformats-officedocument.wordprocessingml.template | Yes | Yes | Yes | Yes | Yes | .dotx |
||||||||

## Microsoft Works

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.ms-works-ss | Yes | Yes | No | No | No | .wps |
| application/vnd.ms-works-wp | Yes | Yes | No | No | No | .wps |
||||||||

## Open Document Format

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.oasis.opendocument.text | Yes | Yes | Yes | Yes | Yes | .odt |
||||||||

## Other

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/json | Yes | Yes | Yes | Yes | Yes | n/a |
| application/vnd.ms-graph | Yes | Yes | No | No | No |  |
| application/winhlp | Yes | Yes | No | No | No | .hlp |
| application/x-tnef | Yes | Yes | No | No | No |  |
||||||||

## Plain Text

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| text/csv | Yes | Yes | Yes | Yes | Yes | .csv |
| text/plain | Yes | Yes | Yes | Yes | Yes | .con; .css; .csv; .dat; .pl; .txt |
||||||||

## Portable Document Format

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/pdf | Yes | Yes | Yes | Yes | Yes | .pdf |
||||||||

## Word Perfect

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.wordperfect; version=5.0 | Yes | Yes | Yes | No | No | .wpd |
| application/vnd.wordperfect; version=5.1 | Yes | Yes | Yes | No | No | .wpd |
| application/vnd.wordperfect; version=6.x | Yes | Yes | Yes | No | No | .wpd |
||||||||

## Word Pro

| Mime type | File identification | Metadata extraction | Text extraction | Native viewer | Annotate viewer | Possible Extensions |
| :- |  :- |  :- |  :- |  :- |  :- |  :- |
| application/vnd.lotus-wordpro | Yes | Yes | No | No | No | .lwp |
||||||||
