ps_pagination
=============
##http://phpsense.com
##Main Features

Ease of integration with existing PHP applications
Easy to customize. The main class is just 200 code lines
Append custom parameters to pagination links
Flexibility in rendering pagination links
##Usage Instructions

#Step One

The first step is to include the ps_pagination.php file in your script.

#Step Two

Create a PS_Pagination object. The PS_Pagination class constructor takes five parameters:

MySQL connection link
SQL query
Number of records to display per page. Defaults to 10
Number of pagination links to display. Defaults to 5
Your own custom parameters you want to be appended to pagination links
The first two are compulsory while the last three are optional.

#Step Three

Next, call the paginate() function. This function returns a paginated result set for the current page. You can use this result set just as you would use a normal MySQL result set.

#Step Four

The final step is to display the pagination links. You can use the renderFullNav() function to generate and display the links in one go or you can use individual function calls to display each link separately.

      
      
      include('ps_pagination.php');
      $conn = mysql_connect('localhost', 'username', 'password');
      mysql_select_db('testdb',$conn);
      $sql = 'SELECT * FROM pages';
      
      //Create a PS_Pagination object
      $pager = new PS_Pagination($conn, $sql, 8, 3);
      
      //The paginate() function returns a mysql result set for the current page
      $rs = $pager->paginate();
      
      //Loop through the result set just as you would loop
      //through a normal mysql result set
      while($row = mysql_fetch_assoc($rs)) {
      echo $row['title'];
      }

      //Display the navigation
      echo $pager->renderFullNav();
How do I use “WHERE”, “ORDER BY” with this class?

You don’t need to pass any special parameters for this to PS_Pagination object. Simply include these in your SQL statement. See below for example.


    //Your SQL Query
    $sql = "select title from product WHERE product_type = 'Digital' ORDER BY title ASC ";

    //Create a PS_Pagination object and pass the above SQL statement to it
    $pager = new PS_Pagination($conn, $sql, 8, 3, 'param1=valu1&param2=value2');
How do I get the total number of rows?


    //Create a PS_Pagination object
    $pager = new PS_Pagination($conn, $sql, 8, 3);

    //Total number of rows returned
    echo $pager->total_rows;
I want to append my own variables to the pagination links

You can pass your a variable string as the fifth argument while creating the pagination class object. This string will be appended to all pagination links.


    //Create a PS_Pagination object
    $my_variables = 'param_1=value_1&param_2=value_2';
    $pager = new PS_Pagination($conn, $sql, 8, 3, $my_variables);
##Functions Overview

      renderFirst – This function displays the link to the first page
      renderLast – This function displays the link to the last page
      renderNext – This function displays link to next page
      renderPrevious – This function displays link to previous page
      renderNav – Displays the page links
      renderFullNav – This function displays all the pagination links in one go
