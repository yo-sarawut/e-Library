# sort\_table\_desc

&lt;!DOCTYPE html&gt;

Sort a HTML Table Alphabetically  
table {  
  border-spacing: 0;  
  width: 100%;  
  border: 1px solid \#ddd;  
}  
  
th {  
  cursor: pointer;  
}  
  
th, td {  
  text-align: left;  
  padding: 16px;  
}  
  
tr:nth-child\(even\) {  
  background-color: \#f2f2f2  
}  


**Click the headers to sort the table.**

The first time you click, the sorting direction is ascending \(A to Z\).

Click again, and the sorting direction will be descending \(Z to A\):

| Name | Country |
| :--- | :--- |
| Berglunds snabbkop | Sweden |
| North/South | UK |
| Alfreds Futterkiste | Germany |
| Koniglich Essen | Germany |
| Magazzini Alimentari Riuniti | Italy |
| Paris specialites | France |
| Island Trading | UK |
| Laughing Bacchus Winecellars | Canada |

  
function sortTable\(n\) {  
  var table, rows, switching, i, x, y, shouldSwitch, dir, switchcount = 0;  
  table = document.getElementById\("myTable"\);  
  switching = true;  
  //Set the sorting direction to ascending:  
  dir = "asc";   
  /\*Make a loop that will continue until  
  no switching has been done:\*/  
  while \(switching\) {  
    //start by saying: no switching is done:  
    switching = false;  
    rows = table.rows;  
    /\*Loop through all table rows \(except the  
    first, which contains table headers\):\*/  
    for \(i = 1; i &lt; \(rows.length - 1\); i++\) {  
      //start by saying there should be no switching:  
      shouldSwitch = false;  
      /\*Get the two elements you want to compare,  
      one from current row and one from the next:\*/  
      x = rows\[i\].getElementsByTagName\("TD"\)\[n\];  
      y = rows\[i + 1\].getElementsByTagName\("TD"\)\[n\];  
      /\*check if the two rows should switch place,  
      based on the direction, asc or desc:\*/  
      if \(dir == "asc"\) {  
        if \(x.innerHTML.toLowerCase\(\) &gt; y.innerHTML.toLowerCase\(\)\) {  
          //if so, mark as a switch and break the loop:  
          shouldSwitch= true;  
          break;  
        }  
      } else if \(dir == "desc"\) {  
        if \(x.innerHTML.toLowerCase\(\) &lt; y.innerHTML.toLowerCase\(\)\) {  
          //if so, mark as a switch and break the loop:  
          shouldSwitch = true;  
          break;  
        }  
      }  
    }  
    if \(shouldSwitch\) {  
      /\*If a switch has been marked, make the switch  
      and mark that a switch has been done:\*/  
      rows\[i\].parentNode.insertBefore\(rows\[i + 1\], rows\[i\]\);  
      switching = true;  
      //Each time a switch is done, increase this count by 1:  
      switchcount ++;        
    } else {  
      /\*If no switching has been done AND the direction is "asc",  
      set the direction to "desc" and run the while loop again.\*/  
      if \(switchcount == 0 && dir == "asc"\) {  
        dir = "desc";  
        switching = true;  
      }  
    }  
  }  
}  


> [Source : ](https://).

