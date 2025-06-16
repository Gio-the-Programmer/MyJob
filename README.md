#MY JOB 

PROGRAM 1
INPUT A2, FLEXCELL0 =IFERROR(INDEX(FILTER(SPLIT($A$2, " "), REGEXMATCH(SPLIT($A$2, " "), "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}")),ROW()-1),"No email detected"),
DEPENDENTCELL0|FLEXCELL0|TOUCHAA2 =IFERROR(LEFT(AA2, FIND("@", AA2) - 1), ""),
DEPENDENTCELL1|DEPENDENTCELL0|TOUCHAB2=IF(AB2="", , LET(uname, AB2,parts, SPLIT(uname, "."),maskPart, LAMBDA(part,LET(len, LEN(part),IF(len = 1, "*",IF(len = 2, LEFT(part, 1) & "*",IF(len = 3, LEFT(part, 1) & "*" & RIGHT(part, 1),IF(len = 4, LEFT(part, 1) & "**" & RIGHT(part, 1),IF(len = 5, LEFT(part, 1) & "***" & RIGHT(part, 1),IF(len = 6, LEFT(part, 1) & "***" & RIGHT(part, 2),IF(len = 7, LEFT(part, 1) & "***" & RIGHT(part, 3),LEFT(part, 3) & REPT("*", MAX(3, len - 6)) & RIGHT(part, 3)))))))))),maskedParts, MAP(parts, maskPart),TEXTJOIN(".", TRUE, maskedParts)))
