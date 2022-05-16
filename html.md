how to make some radio buttons group together? which means user could only select one at a time:
by using name propoerty
radio buttons with same name property are considerd in a same group.
https://www.w3schools.com/tags/tryit.asp?filename=tryhtml5_input_type_radio

```html
<!DOCTYPE html>
<html>
<body>

<h1>Display Radio Buttons</h1>

<form action="/action_page.php">
  <p>Please select your favorite Web language:</p>
  <input type="radio" id="html" name="fav_language" value="HTML">
  <label for="html">HTML</label><br>    
  <input type="radio" id="css" name="fav_language" value="CSS">
  <label for="css">CSS</label><br>
  <input type="radio" id="javascript" name="fav_language" value="JavaScript">
  <label for="javascript">JavaScript</label>

  <br>  

  <p>Please select your age:</p>
  <input type="radio" id="age1" name="age" value="30">
  <label for="age1">0 - 30</label><br>
  <input type="radio" id="age2" name="age" value="60">
  <label for="age2">31 - 60</label><br>  
  <input type="radio" id="age3" name="age" value="100">
  <label for="age3">61 - 100</label><br><br>
  <input type="submit" value="Submit">
</form>

</body>
</html>

```