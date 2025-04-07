<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Group Policy Objects</h1>
This is a continuation tutorial that outlines the implementation of Group Policy Objects in Active Directory with a focus on Account Lockouts. Im using the same VM's that I created in my previous lab with the sam configurations<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<p><img width="750" alt="Screenshot" src="https://github.com/user-attachments/assets/6b91dcf1-d538-45ed-8862-b4623ac2d73b" /></p>
<p>Log into dc-1 as ken_admin, Go to Start -> Run -> gpmc.msc</p>
<p>Edit the Default Domain Policy</p>

<table>
  <tr>
    <td>
      <img width="785" alt="Screenshot" src="https://github.com/user-attachments/assets/98c530c2-676b-4692-b21a-9bd889c52872" />
    </td>
    <td>
      <img width="1204" alt="Screenshot" src="https://github.com/user-attachments/assets/33776f27-1b7e-4420-983d-498cc1867857" />
    </td>
  </tr>
</table>

<p>Double click on Account Lockout Threshold and set the amount of log in attempts to 5. Click Apply.</p>
<br>
<table>
  <tr>
    <td>
      <img width="855" alt="Screenshot" src="https://i.imgur.com/i1r3hic.png" />
    </td>
    <td>
      <img width="252" alt="Screenshot" src="https://github.com/user-attachments/assets/419568a0-17f4-4216-adbc-1f95cb5a6161" />
    </td>
  </tr>
</table>
<p>Log into client-1 as ken_admin and employ the Group Policy Object (GPO) enter gpupdate /force into PowerShell. Make sure to open PowerShell as administrator. Then log out.</p>
<p>Once updated, try logging into client-1 as any one of the users within the domain but put in the wrong password 6 times. A lockout message should appear.</p>
<br>

<p><img width="756" alt="Screenshot" src="https://imgur.com/a/eujMC18" /></p>
<p>Back in dc-1, oepn Active Directory Users & Computers, in _EMPLOYEES find the user that we locked out (bufu.tec) in this case and unlock their account.</p>

<br>

<p><img width="753" alt="Screenshot" src="https://imgur.com/a/bRsuzjv" />
</p>
<p>After the account is unlocked, try logging into client-1 as that user. </p>
<p>We can also easily reset a users password here by right clicking their name.</p>
<br>

<h3>BONUS</h3>

<img width="454" alt="Screenshot" src="https://i.imgur.com/PYfJ1nb.png" />

<p>Back in client-1 as any user, go to Start and search for Event Viewer but open it as an administrator. We can use ken_admin here.</p>
<br>
<p><img width="1330" alt="Screenshot" src="https://i.imgur.com/B8MRgly.png" /></p>

<p>Event Viewer allows us to view security logs. On the left hand side go to Windows Logs -> Security</p>
<p>Right click on Security and click Find. Enter in the user name we were trying to log in as with the wrong password earlier. We can view the failed log in attempts we made.
</p>
