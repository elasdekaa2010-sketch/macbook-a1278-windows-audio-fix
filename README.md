# Windows Audio Fix for MacBook Pro A1278 / MacBookPro9,2

أداة PowerShell لإنشاء فلاشة UEFI تحمل إصلاح ACPI الذي نجح على جهاز MacBookPro9,2 يعمل بـ Windows 10 Enterprise LTSC 21H2، مع متحكم الصوت Intel <code>PCI\VEN_8086&DEV_1E20&SUBSYS_72708086</code> الذي كان يظهر Code 10.

## حمّل الأداة كاملة

نزّل الملف [MacBook-A1278-Windows-Audio-Fix-source.zip](MacBook-A1278-Windows-Audio-Fix-source.zip) من هذا المستودع، وفكّه في Windows. يحتوي الأرشيف على السكربت والمصادر وملفات EFI المطلوبة وبصمات SHA-256 وإشعارات التراخيص. شغّل الأداة من المجلد المستخرج حتى يكون مجلد Payload بجوار السكربت.

## الخطوات

1. جهّز فلاشة USB فارغة بنظام FAT32، واحفظ أي ملفات تريد الاحتفاظ بها. الأداة لا تهيّئ الفلاشة ولا تمسحها.
2. من المجلد المستخرج شغّل <code>Start-Tool.cmd</code>، أدخل حرف الفلاشة مثل E، وتأكد من الملصق، ثم اكتب COPY.
3. أطفئ الماك. شغّله مع الضغط على Option/Alt واختر EFI Boot الخاص بالفلاشة.
4. عند Shell> نفّذ <code>map -r</code>، وحدّد FS الذي مساره يشير إلى USB. على جهاز الاختبار كان USB هو FS0:. اكتب رقم FS الصحيح ثم:

~~~text
fs0:
\EFI\OC\OpenCore.efi
~~~

5. اختر Windows على القرص الداخلي من قائمة OpenCore. استخدم هذه الطريقة في كل إقلاع يحتاج فيه الصوت إلى الرقعة.

للتراجع، أطفئ الماك وانزع USB ثم أقلع من القرص الداخلي. لا تتغير ملفات Windows أو EFI الداخلي. قد يعود Code 10 من دون الرقعة.

## النطاق

تم تأكيد الصوت على جهاز MacBookPro9,2/A1278 المذكور فقط. قد تنطبق الفكرة على بعض أجهزة Sandy/Ivy Bridge المشابهة، لكنها ليست مضمونة لكل موديل. هذه ليست حزمة تعريف صوت تعمل بعد تشغيل Windows؛ OpenCore يحمّل تعديل SSDT-PCI وBUF0 إلى BUF1 قبل بدء Windows. راجع ملف THIRD-PARTY-NOTICES.md داخل الأرشيف للتراخيص والمصادر.

This product includes software developed by Dortania and OpenCore Legacy Patcher contributors.

## English summary

This repository contains the complete Windows PowerShell USB builder and tested EFI payload in the source ZIP. Download and extract it, run Start-Tool.cmd on an already formatted FAT32 removable USB drive, then boot the Mac from the USB and launch the EFI path shown above from UEFI Shell. The confirmed test is one A1278 / MacBookPro9,2 on Windows 10 Enterprise LTSC 21H2; other systems are not guaranteed. The script never formats a drive or modifies the internal Windows installation.
