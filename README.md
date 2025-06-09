# MyJob
Nothing to say

=ARRAYFORMULA(
  IF(A2 = "",
    TRANSPOSE(FILTER(TEXT(SEQUENCE(1, COUNTA(I1:1)-COUNTIF(I1:1, "")), "00") & "% | " & FILTER(I1:1, I1:1<>""), I1:1<>"" )),
    LET(
      headers, FILTER(I1:1, I1:1 <> ""),
      cols, BYCOL(I2:INDEX(I2:Z, , COUNTA(I1:1)), LAMBDA(col,
        SUMPRODUCT(--ISNUMBER(SEARCH(FILTER(col, col<>""), A2))) / MAX(1, COUNTA(FILTER(col, col<>"")))
      )),
      formatted, TEXT(ROUND(100 * cols), "00") & "% | " & headers,
      TRANSPOSE(formatted)
    )
  )
)

