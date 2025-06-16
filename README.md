#MY JOB
input A1

B1=IFERROR(INDEX(FILTER(SPLIT($A$1, " "), REGEXMATCH(SPLIT($A$1, " "), "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}")),ROW()-1),"No email detected")

C1=IFERROR(LEFT(B1, FIND("@", B1) - 1), "")

D1=IF(C1="", , LET(uname, C1,parts, SPLIT(uname, "."),maskPart, LAMBDA(part,LET(len, LEN(part),IF(len = 1, "*",IF(len = 2, LEFT(part, 1) & "*",IF(len = 3, LEFT(part, 1) & "*" & RIGHT(part, 1),IF(len = 4, LEFT(part, 1) & "**" & RIGHT(part, 1),IF(len = 5, LEFT(part, 1) & "***" & RIGHT(part, 1),IF(len = 6, LEFT(part, 1) & "***" & RIGHT(part, 2),IF(len = 7, LEFT(part, 1) & "***" & RIGHT(part, 3),LEFT(part, 3) & REPT("*", MAX(3, len - 6)) & RIGHT(part, 3)))))))))),maskedParts, MAP(parts, maskPart),TEXTJOIN(".", TRUE, maskedParts)))

E1=IF(OR(ISBLANK(D1), ISBLANK(B1)), "", D1 & MID(B1, FIND("@", B1), LEN(B1)))
