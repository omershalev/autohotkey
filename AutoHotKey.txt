; ===================== Functions =====================

OpenDocument(documentPath, windowTitle)
{
	IfWinExist, %windowTitle%
	{
		WinActivate
	}
	else
	{
		Run %documentPath%
	}
	return
}

SwitchToProgram(programName)
{
	SetTitleMatchMode 2
	IfWinExist, %programName%
	{
		WinActivate
	} 
	else 
	{
		Run %programName%
	}
	return

}
; ===================== Hotkeys =====================

; ****** Switch to Outlook ******
^#m::
SwitchToProgram("Outlook")
return

; ****** Switch to OneNote ******
^#o::
SwitchToProgram("OneNote")
return

; ****** Switch to Chrome ******
^#c::
SwitchToProgram("Chrome")
return

; ****** Open Document directory ******
^#d:: Run D:\Documents

; ****** Open Dropbox directory ******
^#p:: Run D:\Dropbox\Dropbox

; ****** Google Translate ******
^#r:: Run chrome.exe https://translate.google.co.il/#auto/iw/%clipboard%

; ****** Launch the path/url in the clipboard ******
^#=::
If InStr(clipboard, "htm") or InStr(clipboard, "asp") or InStr(clipboard, "http")
{
	Run chrome.exe %clipboard%
} 
else
{
	IfExist, %clipboard%
		Run %clipboard%
}
return

; ****** Open dialog box for useful documents and webpages ******
^#u::
text = 
(
Choose the document/website you wish to open:
==============================
s - SomeDocument.txt
a - AnotherDocument.docx
y - YetAnotherDocument.xlsx
)
InputBox, input, Useful, %text%,,,300,,,,40,
if ( input == "s" ) {
    OpenDocument("<path to SomeDocument.txt>", "SomeDocument - Notepad")
} else if (input == "a") {
    OpenDocument("<path to AnotherDocument.docx", "AnotherDocument.docx - Word")
} else if (input == "y") {
    OpenDocument("<path to YetAnotherDocument.xlsx", "YetAnotherDocument - Excel")
} else {
	msgbox Invalid Option
}
return

; ****** Change mouse position ******
^#Left:: MouseMove, -200, 0, 0, R
^#Right:: MouseMove, 200, 0, 0, R
^#Up:: MouseMove, 0, -200, 0, R
^#Down:: MouseMove, 0, 200, 0, R
^!#Left:: MouseMove, -30, 0, 0, R
^!#Right:: MouseMove, 30, 0, 0, R
^!#Up:: MouseMove, 0, -30, 0, R
^!#Down:: MouseMove, 0, 30, 0, R
^+!#Left:: MouseMove, -10, 0, 0, R
^+!#Right:: MouseMove, 10, 0, 0, R
^+!#Up:: MouseMove, 0, -10, 0, R
^+!#Down:: MouseMove, 0, 10, 0, R

; ****** Click mouse and hold ******
;~LShift & RShift:: MouseClick , , , , , , D,

; ****** Release mouse ******
;~RShift & LShift:: MouseClick , , , , , , U,

; ****** Mouse click at the current position ******
*#Enter:: MouseClick
*!#Enter:: MouseClick

; ****** Right mouse click at the current position ******
#\:: MouseClick, right
*!#\:: MouseClick, right
