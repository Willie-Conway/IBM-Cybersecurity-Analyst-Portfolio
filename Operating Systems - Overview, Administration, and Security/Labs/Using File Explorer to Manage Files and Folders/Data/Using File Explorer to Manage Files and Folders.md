
![alt text](<../Screenshots/Windows Defender.png>)


# Hands-on Lab: Using File Explorer to Manage Files and Folders

**Estimated time needed:** 20 minutes

---

## Learning Objectives

In this hands-on lab, you will:

- Employ Microsoft Windows File Explorer for file and folder navigation
- Construct a new folder called "Office files"
- Use LibreOffice to create a new document and add text to that document
- Use the "Office files" folder structure as the LibreOffice document file location
- Identify the stored path of the new document

---

## Important Notices about This Lab

### About Lab Sessions

Lab sessions are **not persisted**. This means that every time you connect to this lab, a new environment is created for you. Any data or files you saved in a previous session are no longer available. To avoid losing your data, plan to complete these tasks in a single session.

### About the Lab Instructions and Solutions

In case you try to use your physical keyboard in the lab environment, it might not produce any visible results. To avoid this issue, please use the **On-Screen Keyboard** (you can find it by searching for "On-Screen Keyboard" in the search bar at the bottom of your screen). If search functionality doesn't work, you can also click on the Windows icon, scroll down to find Windows Ease of Access, click on it, and then select On-Screen Keyboard.

Microsoft Windows operating system features can vary based on the Windows edition. If completing these exercises on your machine, your navigation and solutions may differ from what's presented in this lab.

---

## Exercise 1: Employ Microsoft Windows File Explorer for File and Folder Navigation

In this exercise, you will learn to navigate through Windows File Explorer to locate and manage your files and folders.

### Step 1: Open File Explorer

1. Locate the **File Explorer** icon on your taskbar (usually looks like a folder)
2. Click on the icon to open File Explorer

*Alternatively, you can press **Windows key + E** on your keyboard to open File Explorer directly*


![alt text](<../Screenshots/File Explorer icon on taskbar.png>)

### Step 2: Navigate to Documents

1. In File Explorer, look at the left sidebar (navigation pane)
2. Locate and click on **Documents** (often under "This PC" or "Quick Access")
3. The main pane will now display the contents of your Documents folder


![alt text](<../Screenshots/File Explorer with Documents folder selected.png>)

### Step 3: Explore File Explorer Features

Take a moment to familiarize yourself with File Explorer's key features:

| Feature                   | Location         | Purpose                        |
| :------------------------ | :--------------- | :----------------------------- |
| **Navigation pane** | Left sidebar     | Quick access to common folders |
| **Address bar**     | Top of window    | Shows current location/path    |
| **Search box**      | Top-right corner | Search for files and folders   |
| **View tab**        | Top ribbon       | Change how files are displayed |
| **Column headers**  | In file list     | Sort files by name, date, etc. |

---

## Exercise 2: Construct a New Folder Called "Office files"

In this exercise, you will create a new folder to organize your documents.

### Step 1: Navigate to Documents Folder

1. Ensure you are still in the **Documents** folder from Exercise 1
2. If you navigated away, use the left sidebar to click on **Documents** again

### Step 2: Create a New Folder

There are three ways to create a new folder. Choose any method below:

**Method 1: Right-click method**

1. Right-click on an empty area in the main pane (white space)
2. Hover over **New** in the context menu
3. Click **Folder**


![alt text](<../Screenshots/Right-click menu showing New - Folder.png>)

**Method 2: Ribbon method**

1. Click the **Home** tab in the top ribbon
2. Click **New Folder** in the toolbar

**Method 3: Keyboard shortcut**

1. Press **Ctrl + Shift + N** on your keyboard

### Step 3: Name the Folder

1. A new folder will appear with the name "New folder" highlighted
2. Type the folder name: **`Office files`**
3. Press **Enter** to confirm the name


![alt text](<../Screenshots/New folder being named  - Office files.png>)

### Step 4: Verify Folder Creation

1. You should now see a folder named **Office files** in your Documents folder
2. The folder icon will appear as a standard yellow folder


![alt text](<../Screenshots/Office files folder showing Project 1 Document.png>)

---

## Exercise 3: Use LibreOffice to Create a New Document and Add Text

In this exercise, you will use LibreOffice (a free office suite) to create a document and save it in your new folder.

### Step 1: Open LibreOffice

1. Click the Windows **Start** button (bottom-left corner)
2. Scroll through the applications list or type **LibreOffice** in the search bar
3. Click on **LibreOffice** to open the application


![alt text](<../Screenshots/Start menu with LibreOffice selected.png>)

### Step 2: Select Document Type

1. When LibreOffice opens, you'll see the start center with various document types
2. Click on **Writer Document** to create a new text document


![alt text](<../Screenshots/LibreOffice start center with Writer Document highlighted.png>)

### Step 3: Add Text to the Document

1. A blank document will open in LibreOffice Writer
2. Type the following text in the document:

```
Project 1 - Office Files Lab
Created on: [Current Date]

This document was created as part of the hands-on lab 
learning how to manage files and folders using Windows 
File Explorer and LibreOffice.
```

3. Replace `[Current Date]` with today's date (e.g., February 28, 2026)

![alt text](<../Screenshots/LibreOffice Writer with text entered.png>)

### Step 4: Save the Document to Your Office Files Folder

1. Click on **File** in the top menu bar
2. Select **Save As** from the dropdown menu


![alt text](<../Screenshots/File menu with Save As selected.png>)

1. The Save dialog box will appear
2. Navigate to your **Documents** folder using the left sidebar or address bar
3. Double-click on the **Office files** folder to open it


![alt text](<../Screenshots/Save dialog showing Office files folder.png>)

1. In the **File name** field, type: **`Project 1 Document`**
2. Ensure the file type is set to **ODF Text Document (.odt)** or similar
3. Click **Save**


![alt text](<../Screenshots/Save dialog with filename entered.png>)

### Step 5: Verify the Document Was Saved

1. The document title bar should now show the filename: **Project 1 Document - LibreOffice Writer**
2. This confirms your document has been saved successfully

---

## Exercise 4: Identify the Stored Path of the New Document

In this exercise, you will locate and identify the full file path of your newly created document.

### Step 1: Return to File Explorer

1. Click back on the File Explorer window (or open a new one with **Windows key + E**)
2. Navigate to **Documents** > **Office files**

### Step 2: Locate Your Document

1. In the **Office files** folder, you should see your **Project 1 Document.odt** file
2. The file icon will look like a LibreOffice Writer document


![alt text](<../Screenshots/Office files folder showing Project 1 Document.png>)

### Step 3: Identify the File Path

There are several ways to identify the full file path:

**Method 1: Address Bar**

1. Look at the address bar at the top of File Explorer
2. It should show: **This PC > Documents > Office files**
3. Click in the address bar to see the full path: **`C:\Users\[YourUsername]\Documents\Office files`**

![File Explorer address bar showing full path]

**Method 2: File Properties**

1. Right-click on **Project 1 Document.odt**
2. Select **Properties** from the context menu
3. In the Properties window, look for **Location** - this shows the folder path
4. The full path combines the Location + Filename

![File Properties showing location]

**Method 3: Copy Path**

1. Hold the **Shift** key on your keyboard
2. Right-click on **Project 1 Document.odt**
3. Select **Copy as path** from the menu
4. Open Notepad and press **Ctrl + V** to paste the full path

### Step 4: Document the File Path

In Notepad or a text editor, record the full file path for reference:

```
Full file path: _________________________________________________________

Example: C:\Users\Student\Documents\Office files\Project 1 Document.odt
```

---

## Exercise 5: Additional File Management Practice (Optional)

In this exercise, you will practice additional file management skills.

### Step 1: Create a Subfolder

1. Navigate to your **Office files** folder
2. Create a new folder inside it called **"Project Files"**
3. This will help organize multiple project-related documents

![alt text](<../Screenshots/Create a Subfolder.png>)

### Step 2: Copy the Document

1. Right-click on **Project 1 Document.odt**
2. Select **Copy** (or press **Ctrl + C**)
3. Double-click to open the **Project Files** folder
4. Right-click in an empty area and select **Paste** (or press **Ctrl + V**)
5. You now have a copy of your document in the subfolder

### Step 3: Rename the Copied Document

1. Right-click on the copied document
2. Select **Rename**
3. Change the name to **"Project 1 Document - Backup"**
4. Press **Enter** to confirm

### Step 4: Delete a File (Optional)

1. Select one of the duplicate files
2. Press the **Delete** key on your keyboard
3. Confirm deletion if prompted
4. Remember that deleted files go to the Recycle Bin

---

## Exercise 6: Lab Completion Checklist

### Step 1: Verify All Tasks Completed

Use this checklist to ensure you've completed all lab requirements:

| Task                                                          | Completed |
| :------------------------------------------------------------ | :-------- |
| Opened File Explorer                                          | ☐        |
| Navigated to Documents folder                                 | ☐        |
| Created "Office files" folder                                 | ☐        |
| Opened LibreOffice                                            | ☐        |
| Created new Writer document                                   | ☐        |
| Added text to the document                                    | ☐        |
| Saved document as "Project 1 Document" in Office files folder | ☐        |
| Located the file in File Explorer                             | ☐        |
| Identified the full file path                                 | ☐        |
| Documented the file path                                      | ☐        |

### Step 2: Answer Review Questions

1. **What is the full path to your Project 1 Document?**

   ```
   Path: __________________________________________________
   ```
2. **What are two different ways to create a new folder in File Explorer?**

   ```
   Method 1: ______________________________________________
   Method 2: ______________________________________________
   ```
3. **Why is it important to organize files into folders?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```
4. **What would happen to your files if you closed the lab environment?**

   ```
   _________________________________________________________________
   _________________________________________________________________
   ```

---

## Troubleshooting Tips

| Issue                                            | Solution                                                                                |
| :----------------------------------------------- | :-------------------------------------------------------------------------------------- |
| **Can't find File Explorer**               | Press Windows key + E on keyboard; or search "File Explorer" in taskbar search          |
| **Keyboard not working in lab**            | Use On-Screen Keyboard: Start > Windows Ease of Access > On-Screen Keyboard             |
| **LibreOffice not installed**              | Check with lab administrator; some lab environments come with LibreOffice pre-installed |
| **Can't save file to Office files folder** | Ensure you created the folder first; verify you have write permissions                  |
| **File path looks different**              | Your username may be different; paths vary by system configuration                      |

---

## Summary of Key Commands

| Action               | Command/Method                                 |
| :------------------- | :--------------------------------------------- |
| Open File Explorer   | Windows key + E                                |
| Create new folder    | Ctrl + Shift + N or Right-click > New > Folder |
| Rename file/folder   | Right-click > Rename or select + F2            |
| Copy file            | Ctrl + C                                       |
| Paste file           | Ctrl + V                                       |
| Save document        | Ctrl + S                                       |
| Save As              | F12 or File > Save As                          |
| View file properties | Right-click > Properties                       |
| Copy full path       | Shift + Right-click > Copy as path             |

---

## Key Takeaways

- **File Explorer** is Windows' built-in tool for managing files and folders
- **Folders help organize** documents and make them easier to find
- **File paths** identify exactly where a file is stored (e.g., `C:\Users\Name\Documents\Office files\Project 1 Document.odt`)
- **LibreOffice** is a free alternative to Microsoft Office for creating documents
- **Saving files** to the correct location ensures you can find them later
- **Lab sessions are temporary** - files created in this lab will not persist after you close the session

---

## Summary

In this hands-on lab, you have:

| Activity                                                              | Completed |
| :-------------------------------------------------------------------- | :-------- |
| Opened and navigated File Explorer                                    | ✓        |
| Located the Documents folder                                          | ✓        |
| Created a new folder named "Office files"                             | ✓        |
| Opened LibreOffice Writer                                             | ✓        |
| Created a new document and added text                                 | ✓        |
| Saved the document to the Office files folder                         | ✓        |
| Located the saved document in File Explorer                           | ✓        |
| Identified the full file path of the document                         | ✓        |
| Documented the file path for reference                                | ✓        |
| Practiced additional file management skills (copy, rename, subfolder) | ✓        |

---

## Additional Practice Ideas

1. Create additional folders for different types of documents (Personal, Work, Projects)
2. Create multiple documents and practice moving them between folders
3. Use the search feature in File Explorer to find files by name or content
4. Practice different view modes (Details, List, Icons) in File Explorer
5. Learn to use file properties to add tags and descriptions

---

## Congratulations!

You have successfully completed the **Using File Explorer to Manage Files and Folders** lab. You now know how to:

- Navigate Windows File Explorer
- Create and organize folders
- Use LibreOffice to create documents
- Save files to specific locations
- Identify and document file paths

These fundamental skills are essential for effective computer use and will serve as a foundation for more advanced file management and security tasks.
