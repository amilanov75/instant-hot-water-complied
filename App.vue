/* This is an extract from my App.Vue file. The styles are required to format the single file component accurately */

<style lang="scss">
 
/*  .  = element by it's CLASS                  */  
/*  #  = element by it's ID                     */  
/*     = element by it's HTML TAGS eg DIV, P    */  
 
 :root{
  // ***************** APP  ***************** 
  --body-background-colour: #1c1c1c;
  --card-background-colour: #1f1f1f;
  --button-background-colour: #2e2e2e;
  --box-shadow: #000;
  --box-shadow-buttons: #0f0f0f;
  
}


#app {
  font-family: "Barlow", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  margin-top: 20px;
}

/*WEB PAGE BODY FORMATS*/
body {
  background-color: var(--body-background-colour) !important;
  font-family: "helvetica" !important;
  font-size: 15px !important;
}

/* MAIN BUTTONS USED EVERYWHERE */
button{
  color: #c2c2c2;
  background-color: var(--button-background-colour);
  border: transparent;
  border-radius: 4px;
  font-size:13px !important;
  border-radius: 4px !important;
  padding: 4px 20px;
  width: 80%;
  box-shadow: 0 10px 12px 0 var(--box-shadow-buttons) !important;
}

/*  Colours for Syntax Highlighted pre's */
.syntax-highlight {color:white;background-color:black;padding:5px 10px;}
.syntax-highlight > .key {color:#ffbf35}
.syntax-highlight > .string {color:#5dff39;}
.syntax-highlight > .number {color:#70aeff;}
.syntax-highlight > .boolean {color:#b993ff;}


</style>
