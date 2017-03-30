<!DOCTYPE html PUBLIC "-/W3C/DTD XHTML 1.0 Strict/EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
</head>
<body>

<div id="parentDivId" class="works" >

<form id="FormId1" method="post" >

Enter URL : <input id="inputUrlText" type="text" name="url"/><hr/>

<input id="submitFormBtnId12" type="submit" name="btnSubmit" text="Submit" value="SUBMIT"/>

</form>
</div>

<?php
set_time_limit(0);

function retrieve_remote_file_size($url){
$ch = curl_init($url);

curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
curl_setopt($ch, CURLOPT_HEADER, TRUE);
curl_setopt($ch, CURLOPT_NOBODY, TRUE);

$data = curl_exec($ch);
$size = curl_getinfo($ch, CURLINFO_CONTENT_LENGTH_DOWNLOAD);

curl_close($ch);
return $size;
}

if(isset($_POST['btnSubmit']))
{
//check for empty URL
if(empty($_REQUEST['url']))
{
echo "Empty URL..";
die();
}

/*$getUrlContent = file_get_contents($_REQUEST[\'url\']);
file_put_contents(\"test.txt\",$getUrlContent);
*/

//This is the file where we save the information
/*$cmd=\'curl -O -J -L https://drive.google.com/uc?id=0B4fIuYID3dr-aHY2eS1NcHdMeEU\';
https://drive.google.com/uc?id=0Bz7LPEoNglspOE1fWWdFd2MwN3M
exec($cmd,$result);*/

$ch = curl_init();

//$headers = get_headers(\"https://drive.google.com/uc?id=0Bz7LPEoNglspWnBDaU1Cam14ZW8\", true);
$headers = get_headers($_REQUEST['url'], true);
echo "<xmp>";
print_r($headers);
echo "</xmp>";
curl_setopt($ch, CURLOPT_URL, $headers['Location']);
//curl_setopt($ch, CURLOPT_URL, "https://drive.google.com/file/d/0Bz7LPEoNglspOE1fWWdFd2MwN3M/edit");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

//curl_setopt($ch, CURLOPT_NOBODY, 1);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER,0);

$result = curl_exec($ch);
echo "<br/>";

if (curl_errno($ch)) {
echo 'Error:' . curl_error($ch);
}
curl_close ($ch);

echo "<hr/>";
echo "File from GoogleDrive Is :- <hr/>";
if ( isset($headers['Content-Length']) ) {
$size = 'file size:' . $headers['Content-Length'];

$fileName = "";
preg_match_all("/\\w+\\.\\w+/", $headers['Content-Disposition'], $output);

$fileName = $output[0][0];
$fileLocation = $headers['Location'];

file_put_contents($fileName,$result);

}
else {
$size = 'file size: unknown';
$fileName = "";
preg_match_all("/\\w+\\.\\w+/", $headers['Content-Disposition'], $output);

$fileName = $output[0][0];
$fileLocation = $headers['Location'];

file_put_contents($fileName,$result);
}

echo $size;

echo "<pre>";
print_r($result);
echo "</pre>";
}

?>

</html>
