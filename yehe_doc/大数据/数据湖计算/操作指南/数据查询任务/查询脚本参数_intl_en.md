Data Lake Compute allows you to configure date parameters to facilitate queries with scripts.
Data Lake Compute adopts the standard date format of `yyyymmddhh24miss` and uses the `${}` command to set a date as a variable consisting of the date and time.
- Date: It can be in any date format or a predefined system variable, such as `yyyymmdd`, `yyyymm`, `yyyy-mm-dd`, `yy`, and `dataDate`.
- Time: It can be +/-N cycles and supports `N/Nd`, `Nm`, `Nw`, `Nh`, and `Nmi`. It is compatible with various calculation formulas, such as `7*N` and `N/24`.
Examples

| +/- N Cycle | Method | Compatible Format | Example | 
|---------|---------|---------|---------|
| N years later 	| ${yyyymmdd+Ny}|-| -| 
| N years ago	| ${yyyymmdd-Ny}	| -	| One year ago: ${yyyymmdd-12m}: 20190920| 
| N months later	| -| ${yyyymmdd+Nm}	| -| $[add_months(yyyymmdd,N)]	| -| 
| N months ago	| ${yyyymmdd-Nm}	| $[add_months(yyyymmdd,-N)]	| <nobr>${yyyymmdd-1m}: 20200820<br>${yyyymm}: 202009<br>${dataDate-1m}: 20200820| 
| N weeks later	| ${yyyymmdd+Nw}	| ${yyyymmdd+7*N}	| -| 
| N weeks ago | 	${yyyymmdd-Nw}	| ${yyyymmdd-7*N}	| -| 
| N days later | 	${yyyymmdd+N/Nd}	| 	-| -| 
| N days ago 	| ${yyyymmdd-N/Nd}		| -| ${yyyymmdd-1}, ${dataDate-1}| 
| N hours later 	| ${yyyymmddhh24+Nh}	| $[yyyymmddhh24+N/24]	| -| 
| N hours ago 	| ${yyyymmddhh24-Nh}	| $[yyyymmddhh24-N/24]	| <nobr>${yyyymmddhh24-1h}: 2020092014<br>${dataDate-1h}: 2020092014| 
| N minutes later 	| ${yyyymmddhh24mi+Nmi}	| $[yyyymmddhh24+N/24/60]	| -| 
| N minutes ago 	| ${yyyymmddhh24mi-Nmi}	| $[yyyymmddhh24-N/24/60]| 	${yyyymmddhh24mi-10mi}, ${dataDate-10mi}| 

>! Make sure that the variable or the part before `+/-` in the variable is in line with the standard date format; otherwise, the system cannot recognize and use it.
