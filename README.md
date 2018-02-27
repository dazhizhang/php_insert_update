# php_insert_update

<?php
/*
http://www.w3school.com.cn/php/php_mysql_connect.asp
*/

if (!isset($_GET['acc'])) {
	echo "did not set account, return</br>";
	return;
}
if (!isset($_GET['last'])) {
	echo "did not set lastupdate, return</br>";
	return;
}
if (!isset($_GET['api'])) {
	echo "did not set apivalid, return</br>";
	return;
}
if (!isset($_GET['n'])) {
	echo "did not set note, return</br>";
	return;
}

$acc = $_GET['acc'];
echo $acc;
echo "</br>";
$last = $_GET['last'];
$api = $_GET['api'];
$n = $_GET['n'];

$servername = "localhost";
$username = "root";
$password = "";
 
// 创建连接
$conn = mysql_connect($servername, $username, $password);
if (!$conn) {
    die("Connection failed: " );
}
echo "Connection succeed</br>";

$db_selected = mysql_select_db('monitor', $conn );

if (!$db_selected) {
    die ('Can\'t use monitor : ' . mysql_error());
}
else {
	echo "Use monitor succeed</br>";
}

$query = sprintf("SELECT * FROM modifyprice 
    WHERE account='%s' ",
mysql_real_escape_string($acc));

$result = mysql_query($query);
$row = mysql_fetch_assoc($result);

if (!$result || !$row) {
	echo "inserting</br>";
	
	$query = sprintf("INSERT INTO `monitor`.`modifyprice` (account, lastupdate, apivalid, note) VALUES ('%s', '%s', '%s', '%s') ",
	mysql_real_escape_string($acc),
	mysql_real_escape_string($last),
	mysql_real_escape_string($api),
	mysql_real_escape_string($n)
	);
    $result = mysql_query($query);
/*	mysql_query("INSERT INTO `monitor`.`modifyprice` (acc, last, api, n) VALUES ($acc, $last, $api, $n) ");  */

}
else {
	echo "item already exit, update it</br>" + $result;
	$query = sprintf("UPDATE modifyprice SET  last ='%s' , api ='%s' , n ='%s'
		WHERE acc='%s' ",
		mysql_real_escape_string($last),
		mysql_real_escape_string($api),
		mysql_real_escape_string($n),
		mysql_real_escape_string($acc));
	$result = mysql_query($query);
}

echo (mysql_error());

mysql_close($conn);

?>

http://127.0.0.1/pricemonitor/index.php?acc=oiopoo&last=19888898&api=true&n=hklhjl
