<svelt:head>
	  <script>
    let ipinfo;
    document.body.onload = () => {

      var params = new URLSearchParams(window.location.search);
      alertEl = document.querySelector(".alert");
      if (params.has("success")) {
        setIp();
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#4CAF50";
        alertEl.innerHTML +=
          "<strong>Success!</strong> You have been logged in";
      } else if (params.has("error")) {
        setIp();
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#f44336";
        alertEl.innerHTML += "<strong>Error!</strong> " + params.get("error");
      } else if (params.has("iperror")) {
        setIp();
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#f44336";
        alertEl.innerHTML += "<strong>Error!</strong> " + params.get("iperror");
      } else if (params.has("otpsent")) {
        setIp();
        document.getElementById("otp").type = "password";
        document.getElementById("sendOTP").innerText = "Sign In";
        document.getElementById("mobile").value = params.get("otpsent");
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#4CAF50";
        alertEl.innerHTML += "<strong>Success!</strong> OTP Sent";
      } else if (params.has("ipset")) {
          document.getElementById("tabToggle02").click();
          alertEl.style.display = "block";
          alertEl.style.backgroundColor = "#4CAF50";
        alertEl.innerHTML += "<strong>Success!</strong> IP Setup Successfully";
        document.getElementById("ipinput").value = params.get("ipset");
        setIp()
      } else {
        setIp();
      }
    };
    function copyPlaylist() {
      navigator.clipboard.writeText(`http://${ipinfo['ip']}:${ipinfo['port']}/playlist`).then(function () {
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#4CAF50";
        alertEl.innerHTML = "<strong>Success!</strong> Playlist Copyed to clipboard \n" + `http://${ipinfo['ip']}:${ipinfo['port']}/playlist`;
        console.log("su");
      }, function (err) {
        console.log("er");
        console.error('Async: Could not copy text: ', err);
        alertEl.style.display = "block";
        alertEl.style.backgroundColor = "#4CAF50";
        alertEl.innerHTML += "<strong>Error!</strong> Error while Copying Playlist to clipboard \n" + `http://${ipinfo['ip']}:${ipinfo['port']}/playlist`;
      });
    }
    async function setIp() {
        let data = await fetch('/ip');
        ipinfo = await data.json();
        // document.getElementById("copyPlaylist").innerText = `http://${ipinfo['ip']}:${ipinfo['port']}/playlist`;
        document.getElementById("ipinput").value = ipinfo['ip'];
    }
  </script>
</svelt:head>


<style>
	.body {
        display: flex;
        justify-content: center;
        font-family: Roboto, Arial, sans-serif;
        font-size: 15px;
        color: #ffffff;
      }
      .body {
        background-image: url(https://jiotv.com/src/resources/images/Redirection-screen_Background.jpg);
        background-size: cover;
		height: 92.5vh
	}
      /* form {
        margin-top: 50px;
      } */
      input[type="text"],
      input[type="password"] {
        width: 100%;
        padding: 16px 8px;
        margin: 8px 0;
        display: inline-block;
        border: 1px solid #ccc;
        box-sizing: border-box;
      }
      button {
        background-color: #8ebf42;
        color: white;
        padding: 14px 0;
        margin: 10px 0;
        border: none;
        cursor: pointer;
        width: 100%;
      }
      .a {
        background-color: #8ebf42;
        color: white;
        padding: 14px 0;
        margin: 10px 0;
        border: none;
        cursor: pointer;
        width: 100%;
        text-decoration: none;
        justify-content: center;
        flex: auto;
      }
      h1 {
        text-align: center;
        font-size: 2rem;
        color: #ffffff;
      }
      button:hover {
        opacity: 0.8;
      }
      a:hover {
        opacity: 0.8;
      }
      .formcontainer {
        text-align: left;
        margin: 24px 50px 12px;
      }
      .container {
        padding: 16px 0;
        text-align: left;
      }
      span.psw {
        float: right;
        padding-top: 0;
        padding-right: 15px;
      }
      .alert {
        padding: 20px;
        color: white;
      }

      .closebtn {
        margin-left: 15px;
        color: white;
        font-weight: bold;
        float: right;
        font-size: 22px;
        line-height: 20px;
        cursor: pointer;
        transition: 0.3s;
      }

      .closebtn:hover {
        color: black;
      }
      /* Change styles for span on extra small screens */
      @media screen and (max-width: 300px) {
        span.psw {
          display: block;
          float: none;
        }
      }

      :root {
        --page-height: 100vh;
        --page-width: 100vw;
        --page-margin: 0;
        --page-padding: 0;
        --page-text-color: #8e9196;
        --page-text-color-hover: rgba(255, 255, 255, 1);
        --page-background-color: #1a1e23;
        --tab-display: grid;
        --tab-background-color: rgba(255, 255, 255, 0.03);
        --display-none: none;
        --box-sizing: border-box;
      }
      *:before,
      *:after,
      *,
      ::after,
      ::before {
        box-sizing: border-box;
      }
      .body {
        justify-content: center;
        margin: var(--page-margin);
        padding: var(--page-padding);
      }
      p {
        padding: 0 1em;
      }
      p span {
        color: var(--page-text-color-hover);
      }

      tab-container {
        display: var(--tab-display);
        margin-top: 50px;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: auto 1fr;
        border: solid rgba(255, 255, 255, 0.03);
        border-radius: 0.5em;
        background-color: var(--page-background-color);
        color: var(--page-text-color);
      }
      input {
        display: none;
      }
      input:checked + label {
        color: var(--page-text-color-hover);
        background-color: rgba(255, 255, 255, 0);
        transition: all 250ms;
      }
      .toggleLabel {
        cursor: pointer;
        transition: color 250ms;
        padding: 1em;
        border-right: solid 2px var(--page-background-color);
        background-color: var(--tab-background-color);
        text-align: center;
        transition: all 250ms;
      }
      .toggleLabel:last-of-type {
        border: none;
      }
      .toggleLabel:hover {
        color: var(--page-text-color-hover);
        background-color: rgba(255, 255, 255, 0.05);
      }

      tab-content {
        display: var(--tab-display);
        grid-column: 1 / -1;
      }

      input#tabToggle01:checked ~ tab-content:not(:nth-of-type(1)),
      input#tabToggle02:checked ~ tab-content:not(:nth-of-type(2)),
      input#tabToggle03:checked ~ tab-content:not(:nth-of-type(3)),
      input#tabToggle04:checked ~ tab-content:not(:nth-of-type(4)) {
        display: none;
      }
    </style>


<div class="body flex flex-col">
	<img
		src="https://jiotv.com/src/resources/images/JioTV_logo.png"
		alt="JioTV Logo"
		width="100px"
		height="100px"
		class="mx-auto"
	/>
	<h1 class="text-3xl font-bold mx-auto title-font text-white">JTVServer admin</h1>
	
	<div class="alert" style="display: none">
		<span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span>
	</div>
	<tab-container>
		<input type="radio" id="tabToggle01" name="tabs" value="1" checked />
		<label class="toggleLabel" for="tabToggle01" checked="checked">JioTV Login</label>
		<input type="radio" id="tabToggle02" name="tabs" value="2" />
		<label class="toggleLabel" for="tabToggle02">IP Setup</label>
		<tab-content>
			<form action="/login" method="POST">
				<div class="formcontainer">
					<div class="container">
						<input id="mobile" name="mobile" type="text" placeholder="Mobile Number" required />
						<input id="otp" name="otp" type="hidden" placeholder="OTP" />
					</div>
					<button id="sendOTP" type="submit">Send OTP</button>
					<p style="text-align: center; font-size: small; opacity: 0.5">JioTV login</p>
				</div>
			</form>
		</tab-content>
		<tab-content>
			<form action="/ip" method="POST">
				<div class="formcontainer">
					<div class="container">
						<input id="ipinput" name="ip" type="text" placeholder="Enter Your IP" required />
					</div>
					<button type="submit">Set IP</button>
					<p style="text-align: center; font-size: small; opacity: 0.5">JioTV IP Setup</p>
				</div>
			</form>
		</tab-content>
	</tab-container>
	<div class="formcontainer">
		<a class="a" href="/playlist/download"><button>Download Playlist</button></a>
		<button id="copyPlaylist" onclick="copyPlaylist()" type="submit">Copy Playlist Url</button>
	</div>
</div>

