# Mapping layered security with AA ecosystem APIs

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Category</b>
      </th>
      <th style="text-align:left"><b>AA</b>
      </th>
      <th style="text-align:left"><b>FIP</b>
      </th>
      <th style="text-align:left"><b>FIU</b>
      </th>
      <th style="text-align:left"><b>Layered Security consideration for Request and Response</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Account Discovery and Linking</td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Account Discover <b>[SR1]</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Account Linking/Delink <b>[SR2]</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Authenticating Link/Delink Request <b>[SR3]</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Consent</td>
      <td style="text-align:left">
        <ul>
          <li>Consent Request</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Posting Consent</li>
        </ul>
      </td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Consent Handle Management</td>
      <td style="text-align:left">
        <ul>
          <li>Consent Status Request</li>
        </ul>
      </td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Getting Consent</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">FI Data Flow</td>
      <td style="text-align:left">
        <ul>
          <li>FI Data &#x2013; Request</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>FI Data &#x2013; Request</li>
        </ul>
      </td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>FI Data - Fetch</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>FI Data - Fetch</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <ul>
          <li>Business Layer Security</li>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Notification</td>
      <td style="text-align:left">
        <ul>
          <li>Linking Status</li>
          <li>Consent Status</li>
          <li>FI Data Status</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Consent Status</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Consent Status</li>
          <li>FI Data Status</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
          <li>Protocol Layer Security</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Monitoring</td>
      <td style="text-align:left">
        <ul>
          <li>Heartbeat API</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Heartbeat API</li>
        </ul>
      </td>
      <td style="text-align:left">&#x3A7;</td>
      <td style="text-align:left">
        <ul>
          <li>Application Layer Security</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

* Security Requirement 1 \[SR1\]: The Account discovery request and response implements the application layer security and protocol layer security. The security goals of implementing the application layer security are authenticating the sender, overcome the man-in-the-middle attack, preserve the integrity of the request and response data. Along with application layer security, the protocol layer security encrypts the request and response body while in transit by using TLSv1.2. In this way, the encryption of payload ensures that the data including PII is a secure during data-in-transit without any additional encryption mechanism for PII.
* Security Requirement 2 \[SR2\]: The Account linking/delinking follows the same security requirements as defined in Security Requirement 1\[SR1\].
* Security Requirement 3 \[SR3\]: The Authenticating link/delink uses GET API call to submit the token for verifying the customer based on industry standard RESTful API design principle. The Application layer security by generating the x-jws-signature on GET URL request ensures that the OTP is submitted by authentic customer and overcome the replay attack. The time-bounded space of OTP is restricted to access only for short time for OTP submission and validation. The payload encryption with api key also ensure that the only authentic requester can call this API to submit the OTP which is non-PII data.



