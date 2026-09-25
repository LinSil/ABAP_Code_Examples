This repository is a bunch of personal things I created in ABAP to keep as a reference or to help with common day to day activities.

Z_Copy_Docx_SLIN

This report was created to streamline my personal development cycle. I liked to keep a personal Word docx where I keep personal notes
on the work that I've done on a particular object. So I would be creating one for everything I work on. So I just made this report to
copy a template docx and create a new folder in the directory I gave and save the blank docx into that new folder.

The report allows the user to search for the file they want to copy, directory that they want the new folder to be created, name of the
new folder, and name of the file when copied into the new folder.

<img width="659" height="105" alt="image" src="https://github.com/user-attachments/assets/42c730f9-0f5f-4b18-815a-050111366a2a" />

The report will only create a new folder if the folder doesn't already exist inside of the given directory, and doesn't error out if it
does exist. It would continue to run and use the existing folder. For gui_upload, I use 'BIN' as filetype because my template has tables
with rows that I would fill based on the work I'm doing so I need 'BIN' to keep the document format correct.

<img width="695" height="146" alt="image" src="https://github.com/user-attachments/assets/aba0ea6b-a524-4977-9d4c-af7a06895757" />

Z_dynamic_select_slin

This was a personal project when I first started as a SAP Developer. I was trying to learn ABAP and I just decided that creating a report
that generated a dynamic select statement, execute it, and display the data would be a hard enough challenge to help me understand ABAP as
a coding language. I've updated this multiple times, so for the first iteration didn't look like this, but I feel like this has been the
cleanest version. Since this was more of a learning experience for me, I don't have any plans to expand on this any further.

This report allows the user to enter a list of table names, "valid fields", field names, join, filter checkbox, and rows. Table name is
simply just the names of the tables you want expose.

Valid fields was something that I designed because I wanted the report to be somewhat smart and would be able to determine join conditions
on its own. Originally, I was going to assume all fields with the same technical name in both tables would be used in join conditions, but
I had an use case in an early object where I couldn't join 2 fields with the same technical name because one of the tables wasn't maintain
properly. So I wanted to be able to catch these cases in this. So I created valid fields to indicate which fields within that table were
valid so that the report knew which fields were allow to be used in joins. I also extended this functionality with the select fields. Since
multiple tables could have fields with the same technical name. How would the report know which field to use if only one of them is
maintained? The report will search for the tables and their list of valid fields, to find which table to get that field in their valid fields.
This input is mapped by index to the list of tables, and formatted as comma separated field names.

Field names are just the names of the fields that the user wants to select from the statement and display.

Join is the list of join types if there are multiple tables inputted by the user. They are mapped by index to list of tables and next index.

Apply filter is something new that I didn't have in earlier iterations. But I found a standard API thanks to AI that allows you to pass table
names into this class and it displays a window where you can choose fields within the tables and input the value to filter by.

Rows display allows you to restrict how much data is consumed from the select statement.

<img width="350" height="184" alt="image" src="https://github.com/user-attachments/assets/7097b746-03aa-4a3f-824b-2b1e07ebbb94" />

In this example screenshot, these selection screen values is basically asking to select belnr from BKPF, where the valid fields from BKPF are
BUKRS, BELNR, and GJAHR.

<img width="352" height="180" alt="image" src="https://github.com/user-attachments/assets/b5d0c6c2-90f3-4e87-849f-2279339d899f" />

Output of this is the following.

<img width="114" height="454" alt="image" src="https://github.com/user-attachments/assets/e640ce3c-b12f-4cb9-a8ed-33d6f9573893" />

Since Field names aren't mapped to any index of the list of tables, you have to enter the fields separately in different rows unlike valid
fields.

<img width="961" height="245" alt="image" src="https://github.com/user-attachments/assets/71d92993-2fef-40d9-8e53-826d0e763d05" />

Here in this adjusted example, I added gjahr as another field I wanted to consume from the select statement. By just adding another field
to field names. The report can dynamically change the output type to include gjahr.

<img width="168" height="443" alt="image" src="https://github.com/user-attachments/assets/da5f5563-917b-4901-8e89-afb325849b76" />

The next change I'll make is to add filter. I just check the checkbox, which will indicate that I want to add filters. When you execute
the report, it will call that standard API to show all possible fields that you can filter by based on the tables in the list of tables.

<img width="358" height="184" alt="image" src="https://github.com/user-attachments/assets/6af0cb31-09ea-4375-9527-d069b1489c18" />

<img width="1097" height="645" alt="image" src="https://github.com/user-attachments/assets/7e9e04f0-c383-4bbe-939c-cd089cf97c29" />

I inputted an invalid document number, belnr. So it resulted in 0 results.

<img width="146" height="52" alt="image" src="https://github.com/user-attachments/assets/f886d4b3-10cf-4f63-93d0-f564a15d204e" />

Now I'm going to make a change to show the joins. I will add BSEG so I add it as a new row in table names.

<img width="962" height="247" alt="image" src="https://github.com/user-attachments/assets/d0789075-7ed8-4837-8d24-364f0a40212a" />

Since Valid Fields is index based off the list of tables. I need to add a new row in Valid fields to indicate which valid fields for
BSEG.

<img width="961" height="249" alt="image" src="https://github.com/user-attachments/assets/de17efcb-694d-4a59-a5f1-3b2311afc092" />

Since there are multiple tables, I need to indicate the join type. I enter 1 for inner join. The list of values are
1. Inner Join
2. Left Outer Join
3. Right Outer Join
4. Cross Join

<img width="354" height="182" alt="image" src="https://github.com/user-attachments/assets/33620709-2a7e-4686-be00-8cc6e79f0c5d" />

Since I kept apply filter checked. The filter window will automatically include the new table I added in the selection screen. I added the
invalid document number belnr, into the field within the new table this time.

<img width="1091" height="644" alt="image" src="https://github.com/user-attachments/assets/74ef02b1-9094-48e6-a2d3-8de5ef54ce91" />

And like last time, because this document number doesn't exist, and it does an inner join with the previous table. It results into no results.

<img width="146" height="47" alt="image" src="https://github.com/user-attachments/assets/7c5b9730-700d-4744-938b-6fc022bb4edc" />

However, if I rerun this but pass a valid document number for document number.

<img width="1097" height="120" alt="image" src="https://github.com/user-attachments/assets/cf80de7b-2eae-49bd-bc13-c34377574494" />

You can see that the inner join produced 2 rows because the second table had 2 rows with that document number.

<img width="156" height="90" alt="image" src="https://github.com/user-attachments/assets/2b33efa7-a457-4481-94c2-480cabe75196" />

Overall, I think this was a pretty good first POC for me to learn. There are still a lot of limitations that I don't plan on resolving. For
example, what if the user wants to join 2 fields with different technical names? There is no logic for this, it has to match technical names
in this current iteration and would add complexity to try to map fields with different technical names.
