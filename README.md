# Highlight_VACCINE_DATA_SQL
This project Shows Emphasizing important information: Highlighting can be used to emphasize important information in a text, Table This can make it easier for readers to scan a text and find the most important Filtered Information.

DAX CODE USED TO HIGHLIGHT:
bar to highlight new = 
var _selectedmonths =
           VALUES( months[month name])
var monthtohighlight =
            SELECTEDVALUE(EASTWESTSOUTHBACKUP[month name])
var filtered = 
             ISFILTERED(months[month name])
return

SWITCH (TRUE, NOT(filtered) ,"Grey", monthtohighlight IN _selectedmonths && filtered,"Yellow","Grey")
