<div align="center">

## \[ A Program That \*Indirectly\* Write Text To Notepad \]


</div>

### Description

A program that writes text to Notepad. The code is fully commented and easy to understand. PLEASE vote for it or comment for it. It takes very little time to comment and it is very appreciated. If you can't vote, the least you can do is comment on it. Tell me if it is bad or good.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Brenton Andrew Saunders](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/brenton-andrew-saunders.md)
**Level**          |Intermediate
**User Rating**    |4.4 (35 globes from 8 users)
**Compatibility**  |Microsoft Visual C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/brenton-andrew-saunders-a-program-that-indirectly-write-text-to-notepad__3-8871/archive/master.zip)

### API Declarations

windows.h


### Source Code

```
#include <windows.h> // Very important. Otherwise this whole thing wouldn't work!
// WriteToNotepad()
// Indirectly writes text to Notepad
// Returns TRUE or FALSE depending on success
BOOL WriteToNotepad(LPCTSTR lpszText)
{
	HWND hwndNotepad; // A handle to the Notepad window
	HWND hwndEdit;  // A handle to Notepad's work area
	// Where's Notepad?
	hwndNotepad = FindWindow("Notepad", NULL);
	// Did we find it?
	if(!hwndNotepad)
	{
		// Guess not
		// Try to run it from the Windows directory
		WinExec("Notepad", SW_SHOWNORMAL);
		// Wait a few milliseconds (If your computer is slow it may take a while)
		Sleep(100);
		// Find it again
		hwndNotepad = FindWindow("Notepad", NULL);
		// Did we find it this time?
		if(!hwndNotepad)
		{
			// Nope.
			// Return FALSE indicating failure :(
			return FALSE;
		}
	}
	// Good, we found Notepad.
	// Now lets find it's the edit control
	// that makes up it work area
	// We'll use FindWindowEx this time because it is used to find
	// child windows
	hwndEdit = FindWindowEx(hwndNotepad, NULL, "Edit", NULL);
	// Success?
	if(!hwndEdit)
	{
		// Oops. Busted.
		// Nothing we can do here. Return FALSE indicating failure (:
		return FALSE;
	}
	// Good, we found the edit control
	// Now we're going to loop through the characters in the lpszText (defined by user)
	// and display them individually
	for(int i = 0; i < lstrlen(lpszText); i ++)
	{
		LRESULT lRet; // We use this to recieve the return value of SendMessage (just in case it fails)
		// Write the characters one by one by sending a WM_CHAR message to
		// the edit control
		lRet = SendMessage(hwndEdit, WM_CHAR, lpszText[i], NULL);
		// Any problems?
		if(!lRet)
		{
			// Nothing we can really do. There's no point in breaking
			// the loop, so ignore it.
		}
	}
	// Good! Everything worked out.
	// Return TRUE indicating success :)
	return TRUE;
}
// main()
// Marks the beginning and end of program execution
// No return value
VOID main()
{
	// Let's give it a try
	// Display "Hello World!" to the user via Notepad
	WriteToNotepad("Hello World!\n");
	/*
	The only drawback of this function is that in order to see what
	was written to Notepad, the user must manually go at bring the
	window to the foreground. While there is a function that can do
	this automatically (SetForegroundWindow()), it won't work because
	the console must be in the foreground in order to, well, RUN!
	Note:
	This function works just as if you were to use cout<< or printf()
	meaning in order to start a new line, you must include a '\n' character
	in the text (as shown above). To delete text, use '\b'
	*/
}
```

