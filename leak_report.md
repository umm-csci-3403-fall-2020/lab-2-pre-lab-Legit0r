# Leak report

46 bytes in 6 blocks are definitely lost in loss record 1 of 1
==83==    at 0x483DD99: calloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==83==    by 0x109271: strip (check_whitespace.c:41)
==83==    by 0x1092E1: is_clean (check_whitespace.c:62)
==83==    by 0x109391: main (check_whitespace.c:87)
==83==
==83== LEAK SUMMARY:
==83==    definitely lost: 46 bytes in 6 blocks
==83==    indirectly lost: 0 bytes in 0 blocks
==83==      possibly lost: 0 bytes in 0 blocks
==83==    still reachable: 0 bytes in 0 blocks
==83==         suppressed: 0 bytes in 0 blocks
==83==
==83== For lists of detected and suppressed errors, rerun with: -s
==83== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)

Allocated by calloc in check_whitespace.c
at line 41 of function strip
at line 62 of function is_clean
at line 87 of function main

Memory leaks whenever is_cleaned calls strip, because strip allocates memory. To fix, you have to
free(cleaned) after strip is used to free up the memory.

