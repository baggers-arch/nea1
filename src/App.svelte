
<script>

//fetch http://127.0.0.1:3000/read1

let url='http://127.0.0.1:3000';

let outputData=[];

let inputUsername = ''
let inputPassword = ''
let password = ''




let findData=(userName)=>{
    //fetch(url+'/find1',{
    fetch(url+'/api/findUser',{
      method:"POST",
      headers:{
        'Accept':'application/json',
        'Content-type':'application/json'
      },
      body:JSON.stringify({user:userName})
      

    }).then(res=>res.json()).then(data=>{
      console.log(data);
      outputData=data.results;
      password=(outputData[0].Password);
      console.log(password)
      if (inputPassword != []){
      checkPassword()}
    });
};



let getTutorData=()=>{
 
  fetch(url+'/find2',{
      method:"POST",
      headers:{
        'Accept':'application/json',
        'Content-type':'application/json'
      },
      body:JSON.stringify({user:inputUsername})
      

    }).then(res=>res.json()).then(data=>{
      console.log(data);
      outputData=data.results;
     
    });

};



let getAllData=()=>{
  //fetch(url+'/read1',{
  fetch('/api/auth',{
  }).then(res=>res.json()).then(data=>{
    console.log('getAllData()');
    console.log(data);
 
  });
}

getAllData();

let checkPassword=()=>{
  if (inputPassword != []){
    if (password === inputPassword) {
      console.log(password === inputPassword)
      window.alert("Password Success") 
        getTutorData();
  
  
    }
    
    else {
      window.alert("Wrong Username or Password")
      console.log(password === inputPassword)}
    }
  else {window.alert("No Password Entered")
  
  }
}

let handleClick=()=>{
  findData(inputUsername)
  
}
  


</script>


<body>
<img src="https://www.planetestream.co.uk/img/case/main-oakham-logo.png">
<input type=string bind:value={inputUsername} placeholder="Username:" required>
<input type=password bind:value={inputPassword} placeholder="Password:"required>
<button on:click={handleClick}>Submit</button>
<p>Welcome! {inputUsername}</p>



</body>
{#if !!outputData[0]}

  <table>
  {#each outputData as row,rowIndex}
    <tr>
      <td>{row.user}</td>
      <td>{row.first}</td>
      <td>{row.last}</td>
      <td>{row.data1}</td>
    </tr>

  {/each}
  </table>


{/if}



{#if !!outputData[0]}
  {JSON.stringify(outputData)}

{/if}


<style>
button:hover {
  opacity: 0.5;
}
body{
  background-image: url("https://i.imgur.com/LkdPhy2.png");
  background-repeat: no-repeat;
  background-size: cover;
}
input{
  font-family: monospace;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
  opacity: 0.5
}
button {
  font-family: monospace;
  font-size: x-large;

  background-color: #e41b36;
  color: rgb(0, 0, 0);
  padding: 14px 20px;
  margin: 10px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}

img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
p {
  font-family: sans-serif;
  text-align: center;
  font-size:xx-large;
  
}

</style>