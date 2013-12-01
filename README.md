college_data_project
====================

<?php
mysql_connect("sql2.njit.edu", "per2", "entrant62") or die("Connection Failed");
mysql_select_db("per2")or die("Connection Failed");

$program = new program();


class program{
    function __construct(){
		$page = 'homepage';
		$arg = NULL;

		if(isset($_REQUEST['page'])) {
  		$page = $_REQUEST['page'];
		}
		
		if(isset($_REQUEST['arg'])) {
		$arg  = $_REQUEST['arg'];
		}
        
        $page = new $page($arg);
	}
	
    function __destruct(){
	}
}

abstract class page{
	public $content;

	function menu() {
		$menu = '<li><a href="./collegeproject.php">Homepage</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question1">Question 1</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question2">Question 2</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question3">Question 3</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question4">Question 4</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question5">Question 5</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question6">Question 6</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question7">Question 7</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question8">Question 8</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question9">Question 9</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question10">Question 10</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question11">Question 11</a> </li>';
		$menu .= '<li><a href="./collegeproject.php?page=question12">Question 12</a> </li>';

		return $menu;
	}

    function __construct($arg = NULL){
        if ($_SERVER['REQUEST_METHOD'] == 'GET'){
            $this->get();
		}
        else{
            $this->post();
		}
	}
    
    function get(){
	}
    
    function post(){
	}

	function __destruct(){
		echo $this->content;
	}  
}

class homepage extends page{
  	
    function get(){
		echo '<h2>Welcome, this is the homepage for the College Data Project</h2> <br>';
		$this->content .= $this->menu();
	}
}
  
  
class question1 extends page{
  		
    function get(){
      	echo '<h2>Question #1</h2>';

		$this->content .= $this->question1table();
	}
	  
	function question1table(){
		$result = mysql_query("SELECT instnm, efytotlt
		FROM effy2011, hd2011
		WHERE effy2011.unitid = hd2011.unitid
		ORDER BY efytotlt DESC 
		LIMIT 10") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Headcount</th> </tr>";

		while($row = mysql_fetch_array( $result )) {

		echo "<tr><td>";
		echo $row['instnm'];
		echo "</td><td>";
		echo $row['efytotlt'];
		echo "</td></tr>";
		} 

		echo "</table>";

	return $result;
	}

	function post(){	
		print_r($_POST);
	}
}

  
class question2 extends page{
    	
    function get(){
		echo '<h2>Question #2</h2>';
		$this->content .= $this->question2table();
	}
	
	function question2table(){
		$result = mysql_query("SELECT hd2011.instnm, liability.f1a13
		FROM hd2011
		INNER JOIN liability ON hd2011.unitid = liability.unitid
		ORDER BY f1a13 DESC limit 25") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Liabilities</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
	
		echo "<tr><td>"; 
		echo $row['instnm'];
		echo "</td><td>"; 
		echo $row['f1a13'];
		echo "</td></tr>"; 
	} 

		echo "</table>";

		return $result;
	}	
	
	function post(){	
		print_r($_POST);
	}
}


class question3 extends page{
    	
    function get(){
      	echo '<h2>Question #3</h2>';
		$this->content .= $this->question3table();
	}
	
	function question3table(){
		$result = mysql_query("SELECT instnm, f1a18
		FROM hd2011, netassets
		WHERE hd2011.unitid = netassets.unitid
		ORDER BY f1a18 DESC 
		LIMIT 30") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Net Assets</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
		echo "<tr><td>";
		echo $row['instnm'];
		echo "</td><td>";
		echo $row['f1a18'];
		echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}
  
  
class question4 extends page{
    function get(){
      	echo '<h2>Question 4</h2>';
		$this->content .= $this->question4table();
	}
	
	function question4table(){
		echo 'Same as question #3';
	}
	
	function post(){	
		print_r($_POST);
	}
  
}
  
  
class question5 extends page{
   	function get(){
   	  	echo '<h2>Question #5</h2>';
		$this->content .= $this->question5table();	
	}

	function question5table(){
		$result = mysql_query("SELECT instnm, f1b25
		FROM hd2011
		INNER JOIN revenue
		ON hd2011.unitid = revenue.unitid
		ORDER BY f1b25 DESC 
		LIMIT 30") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Total Revenue</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>"; 
			echo $row['f1b25'];
			echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}
	
class question6 extends page{
    	function get(){
    	  	echo '<h2>Question #6</h2>';

    	  	$this->content .= $this->question6table();	
		}

	function question6table() {
		$result = mysql_query("SELECT distinctrow instnm, (f1b25 / efytotlt) AS Total
		FROM hd2011, effy2011, revenue
		WHERE hd2011.unitid = effy2011.unitid
		AND hd2011.unitid = revenue.unitid
		AND effy2011.unitid = revenue.unitid
		ORDER BY total DESC limit 10") 
		or die(mysql_error());  

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Total Revenue per Student</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>"; 
			echo $row['instnm'];
			echo "</td><td>"; 
			echo $row['Total'];
			echo "</td></tr>"; 
		} 

		echo "</table>";

		return $result;
	}
	
	function post() {	
		print_r($_POST);
	}
  
}	


class question7 extends page{
    	function get(){
    	  	echo '<h2>Question #7</h2>';

    	  	$this->content .= $this->question7table();
		}

	function question7table(){
		$result = mysql_query("SELECT instnm, (f1a18 / efytotlt) AS Total
		FROM hd2011, effy2011, netassets
		WHERE hd2011.unitid = effy2011.unitid
		AND hd2011.unitid = netassets.unitid
		AND effy2011.unitid = netassets.unitid
		ORDER BY total DESC limit 10") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Total Net Assets per Student</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>";
			echo $row['Total'];
			echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}	


class question8 extends page{
    	function get(){
    	  	echo '<h2>Question #8</h2>';

		$this->content .= $this->question8table();
		}

	function question8table(){
		$result = mysql_query("SELECT instnm, (f1a13 / efytotlt) AS Total
		FROM hd2011, effy2011, liability
		WHERE hd2011.unitid = effy2011.unitid
		AND hd2011.unitid = liability.unitid
		AND effy2011.unitid = liability.unitid
		ORDER BY total DESC limit 10") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Total Liability per Student</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>";
			echo $row['Total'];
			echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}


class question9 extends page{
    	
    function get(){
      	echo '<h2>Question #9</h2>';
		$this->content .= $this->question9table();
	}
	
	function question9table(){
		$result = mysql_query("SELECT INSTNM, efytotlt, f1a13, f1a18, f1b25, 
(f1b25 / efytotlt) AS total, 
(f1a18 / efytotlt) AS net, 
(f1a13/ efytotlt) AS lib
FROM effy2011, hd2011, liability, netassets, revenue
WHERE effy2011.UNITID = hd2011.UNITID
AND liability.UNITID = hd2011.UNITID
AND netassets.UNITID = effy2011.UNITID order by instnm desc limit 5 ") 
or die(mysql_error());  

echo "<table border='1'>";
echo "<tr> <th>College Name</th> <th>ENROLLMENT</th><th>Liab</th><th> Netassets</th><th>Revenues</th><th>T_Revenues</th><th>T_Net</th><th>T_Liab</th></tr>";
// keeps getting the next row until there are no more to get
while($row = mysql_fetch_array( $result )) {
	// Print out the contents of each row into a table
	echo "<tr><td>"; 
	echo $row['INSTNM'];
	echo "</td></tr>"; 
	echo $row['effytotlt10'];
	echo "</td></tr>"; 
	echo $row['f1a13'];
	echo "</td><td>"; 
	echo $row['f1a18'];
	echo "</td><td>"; 
	echo $row['f1b25'];
	echo "</td><td>"; 
	echo $row['total'];
	echo "</td><td>"; 
	echo $row['net'];
	echo "</td><td>"; 
	echo $row['lib'];
	echo "</td></tr>"; 
}
 
		echo "</table>";
		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}


class question10 extends page{
    	function get(){
    	  	echo '<h2>Question #10</h2>';
			

		
		$this->content .= $this->question10table();
		}

	
	function question10table(){
		$form = '<form name= "search" action="collegeproject.php?page=question10" method="post">
    	<P>              
        <INPUT type=text name=find><BR>
    	<INPUT type= submit name= search value= "Search"><BR>
    	</P>
		</form>';
		
		return $form;


		$result = mysql_query("select instnm, stabbr from hd2011 where stabbr LIKE $find");


		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>State</th> </tr>";

		while($row = mysql_fetch_array($result)){
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>";
			echo $row['stabbr'];
			echo "</td></tr>";
} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}


class question11 extends page{
    	function get(){
    	  	echo '<h2>Question #11</h2>';

		$this->content .= $this->question11table();
		}

	function question11table(){
		$result = mysql_query("select instnm,(((liability.f1a13-liability2010.liability10)/liability2010.liability10)*100) as Percentage
from liability, liability2010, hd2011
where liability.unitid= liability2010.unitid
and liability.unitid= hd2011.unitid
and hd2011.unitid= liability2010.unitid
order by Percentage desc limit 10") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Percentage Increase</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>";
			echo $row['Percentage'];
			echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}


class question12 extends page{
    	function get(){
    	  	echo '<h2>Question #12</h2>';

		$this->content .= $this->question12table();
		}

	function question12table(){
		$result = mysql_query("select instnm,(((effy2011.efytotlt-effy2010.efytotlt10)/effy2010.efytotlt10)*100) as Percentage
from effy2011, effy2010, hd2011
where effy2011.unitid= effy2010.unitid
and effy2011.unitid= hd2011.unitid
and hd2011.unitid= effy2010.unitid
order by Percentage desc limit 10") 
		or die(mysql_error());

		echo "<table border='1'>";
		echo "<tr> <th>College Name</th> <th>Percentage Increase</th> </tr>";

		while($row = mysql_fetch_array( $result )) {
			echo "<tr><td>";
			echo $row['instnm'];
			echo "</td><td>";
			echo $row['Percentage'];
			echo "</td></tr>";
		} 

		echo "</table>";

		return $result;
	}
	
	function post(){	
		print_r($_POST);
	}
  
}
?>
