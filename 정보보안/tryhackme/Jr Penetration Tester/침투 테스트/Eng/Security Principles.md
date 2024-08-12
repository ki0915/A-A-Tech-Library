



![[Pasted image 20240812105418.png]]




<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Security Principles and Threat Modeling</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        h1, h2, h3 {
            color: #007bff;
            margin-bottom: 10px;
        }
        h2 {
            color: #0056b3;
            margin-top: 20px;
        }
        h3 {
            margin-top: 20px;
            margin-bottom: 10px;
            color: #333;
        }
        h4 {
            color: #333;
        }
        p, ul {
            margin: 0 0 10px;
        }
        ul {
            padding-left: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table, th, td {
            border: 1px solid #ddd;
        }
        th, td {
            padding: 10px;
            text-align: left;
        }
        th {
            background-color: #007bff;
            color: white;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        .highlight {
            font-weight: bold;
            color: #ff5722;
        }
        .important {
            color: #ff5722;
            font-weight: bold;
        }
        .note {
            color: #28a745;
            font-weight: bold;
        }
        .warning {
            color: #dc3545;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Security Principles</h1>
        
        <h2>1. Introduction</h2>
        <p>Principles of information security to protect data and safeguard systems from abuse.</p>
        
        <h2>2. Principles of Security</h2>
        <p>The model of <span class="highlight">confidentiality</span>, <span class="highlight">integrity</span>, and <span class="highlight">availability</span> (CIA) consists of these three principles and has become an industry standard today. This model helps in making decisions about the value of the data and what is needed in a business.</p>
        
        <h3>Three Elements of Security Principles</h3>

        <h4>Confidentiality</h4>
        
        <p><span class="important">Confidentiality</span> is about protecting data from unauthorized access and misuse. Organizations always store some form of sensitive data within their systems. Providing confidentiality is about protecting this data from unintended access by anyone other than the authorized individuals.</p>
        
        <h4>Integrity</h4>
        
        <p><span class="important">Integrity</span> ensures that data remains unaltered except for authorized changes. Data can be changed due to careless handling, system errors, or unauthorized access. In security principles, integrity is maintained if information remains unchanged during storage, transmission, and usage, ensuring unauthorized individuals cannot alter the data (e.g., data breaches).</p>
        
        <h4>Availability</h4>
        <p>To be useful, data must always be accessible and available to users. <span class="important">Availability</span> is an essential element.</p>
        
        <h2>3. Principle of Least Privilege</h2>
        <p>It is important to manage and correctly define various levels of access to information technology systems that individuals need.</p>
        <p>The level of access granted to individuals is determined by two basic factors:</p>
        <ul>
            <li><span class="highlight">The role/function</span> of the individual within the organization</li>
            <li><span class="highlight">The sensitivity of the information</span> stored in the system</li>
        </ul>
        <p>Two key concepts used in assigning and managing user access rights are <span class="important">PIM (Privileged Identity Management)</span> and <span class="important">PAM (Privileged Access Management)</span>.</p>
        <p>Initially, these two concepts may seem similar. However, they are different. PIM is used to translate user roles within an organization into access roles within the system. In contrast, PAM primarily deals with managing the privileges associated with system access.</p>
        <p>A critical aspect of access and privilege control is the <span class="highlight">principle of least privilege</span>. In simple terms, users should be given only the minimum privileges necessary to perform their duties.</p>
        <p>PAM integrates more than just access assignment. It also includes security policy enforcement such as password management, policy auditing, and reducing the attack surface of systems.</p>
        
        <h2>4. Security Models</h2>
        <p>Before discussing security models in detail, let's consider the three elements of CIA: confidentiality, integrity, and availability.</p>
        <p>According to security models, any system or technology that stores information is referred to as an <span class="highlight">information system</span>, and this is how systems and devices are referenced in this context.</p>
        <p>Let's look at some popular and effective security models used to achieve the three elements of CIA.</p>
        
        <h3>Bell-La Padula Model</h3>
        <p>The <span class="important">Bell-La Padula Model</span> is used to achieve confidentiality. This model assumes a hierarchical structure within an organization where everyone's responsibilities/roles are well defined.</p>
        <p>This model operates by granting access to data (referred to as objects) based on a <span class="highlight">"write-up, read-down"</span> rule. It ensures that individuals can access only the data they need.</p>
        <table>
            <tr>
                <th>Advantages</th>
                <th>Disadvantages</th>
            </tr>
            <tr>
                <td>The model’s policies can be applied to actual organizational hierarchies and vice versa.</td>
                <td>Full confidentiality is not achieved as users may learn about the existence of objects they cannot access.</td>
            </tr>
            <tr>
                <td>Implementation and understanding are straightforward and proven successful.</td>
                <td>The model relies heavily on trust within the organization.</td>
            </tr>
        </table>
        
        <h3>Biba Model</h3>
        <p>The <span class="important">Biba Model</span> is similar to the Bell-La Padula Model but focuses on integrity rather than confidentiality in CIA.</p>
        <p>This model applies rules summarized as <span class="highlight">"write-up, read-down."</span> This means that a subject can write to information at its own level or lower but can only read data at its level or higher.</p>
        <table>
            <tr>
                <th>Advantages</th>
                <th>Disadvantages</th>
            </tr>
            <tr>
                <td>The model is straightforward to implement.</td>
                <td>With multiple levels of access and objects, security levels can easily be overlooked when applying security controls.</td>
            </tr>
            <tr>
                <td>It addresses both confidentiality and data integrity, overcoming some limitations of the Bell-La Padula Model.</td>
                <td>It often causes delays in business operations. For example, in a hospital where this model is applied, a doctor might not be able to read notes written by a nurse, leading to delays.</td>
            </tr>
        </table>
        <p>The Biba Model is used in situations or organizations where integrity is more critical than confidentiality. For example, in software development, developers may need access only to the code necessary for their tasks and not to other critical information.</p>
        
        <h2>5. Threat Modeling and Incident Response</h2>
        <p><span class="important">Threat modeling</span> is the process of reviewing, improving, and testing security protocols in an organization's IT infrastructure and services.</p>
        <p>An important step in the threat modeling process is identifying potential threats and vulnerabilities that a system or application may face.</p>
        <p>The threat modeling process is similar to risk assessments performed in the workplace for employees and customers, following similar principles.</p>
        <ul>
            <li><span class="highlight">Preparation</span></li>
            <li><span class="highlight">Identification</span></li>
            <li><span class="highlight">Mitigation</span></li>
            <li><span class="highlight">Review</span></li>
        </ul>
        <p>To assist, frameworks such as <span class="important">STRIDE</span> (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege) and <span class="important">PASTA</span> (Process for Attack Simulation and Threat Analysis) are available. Below, we will discuss STRIDE in detail. STRIDE, developed by two Microsoft security researchers in 1999, remains influential today. STRIDE includes six key principles.</p>
        
        <table>
            <tr>
                <th>Principle</th>
                <th>Description</th>
            </tr>
            <tr>
                <td>Spoofing</td>
                <td>This principle involves authenticating requests and users accessing the system. Spoofing includes malicious parties pretending to be someone else. Measures such as access keys (e.g., API keys) or encryption through signatures help address this threat.</td>
            </tr>
            <tr>
                <td>Tampering</td>
                <td>This principle involves providing tamper-evident measures to ensure data integrity. Data accessed should be maintained in its original, accurate state, similar to how groceries are sealed to preserve them.</td>
            </tr>
            <tr>
                <td>Repudiation</td>
                <td>This principle directs the use of logging for system or application activities to track services.</td>
            </tr>
            <tr>
                <td>Information Disclosure</td>
                <td>Applications or services handling information from multiple users should be properly configured to only display information relevant to the owner.</td>
            </tr>
            <tr>
                <td>Denial of Service</td>
                <td>Applications and services use system resources, so measures should be taken to prevent the abuse of applications/services from causing the entire system to go down.</td>
            </tr>
            <tr>
                <td>Elevation of Privilege</td>
                <td>This is the worst-case scenario for applications or services, where a user can escalate their privileges to a higher level, such as an administrator. This often leads to further exploitation or information disclosure and is a significant concern in security incidents.</td>
            </tr>
        </table>
        
        <p>Security breaches are referred to as <span class="important">incidents</span>. Despite stringent threat models and secure system designs, incidents do occur. The actions taken to address and remediate threats are known as <span class="important">Incident Response (IR)</span> and are a crucial part of a career in cybersecurity.</p>
        <p>Incident response processes are often covered in security certifications such as those offered by CISA.</p>
        <p>Incidents are classified using urgency and impact ratings. Urgency is determined by the type of attack faced, the location of the affected system, and the impact on business operations.</p>
        <p>Incidents are responded to by <span class="highlight">Computer Security Incident Response Teams (CSIRTs)</span> that are pre-organized with technical knowledge of the current incident. To successfully resolve an incident, the following six steps of incident response are often listed in the table below.</p>
        
        <table>
            <tr>
                <th>Action</th>
                <th>Description</th>
            </tr>
            <tr>
                <td><span class="highlight">Preparation</span></td>
                <td>Are resources and plans in place to handle security incidents?</td>
            </tr>
            <tr>
                <td><span class="highlight">Identification</span></td>
                <td>Have threats and threat actors been correctly identified so that we can respond?</td>
            </tr>
            <tr>
                <td><span class="highlight">Containment</span></td>
                <td>Can the threat/security incident be contained to prevent impact on other systems or users?</td>
            </tr>
            <tr>
                <td><span class="highlight">Eradication</span></td>
                <td>Eliminate the active threat.</td>
            </tr>
            <tr>
                <td><span class="highlight">Recovery</span></td>
                <td>Perform a thorough review of the affected systems to restore normal operations and business.</td>
            </tr>
            <tr>
                <td><span class="highlight">Lessons Learned</span></td>
                <td>What can be learned from the incident? For instance, if it was caused by a phishing email, better training for employees to detect phishing emails should be provided.</td>
            </tr>
        </table>
    </div>
</body>
</html>
