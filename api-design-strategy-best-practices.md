# API Design Strategy Best Practices

The API design of NBFC ecosystem uses the RESTful principle to design the programming interfaces that each of the stakeholders, viz. the FIP, the AA, and the FIU need to host to facilitate the account aggregation functionality. The following HTTP methods are used in the design of AA ecosystem.

<table>
  <thead>
    <tr>
      <th style="text-align:left">HTTP Method</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Request has body</th>
      <th style="text-align:left">Response has body</th>
      <th style="text-align:left">Idempotent</th>
      <th style="text-align:left">Cacheable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">GET</td>
      <td style="text-align:left">
        <p>Requests the representation of a resource.</p>
        <p>The primary information retrieval mechanism.</p>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Yes</td>
    </tr>
    <tr>
      <td style="text-align:left">POST</td>
      <td style="text-align:left">
        <p>Requests server processing of an attached payload according to its own
          semantics.</p>
        <p>Can be used to submit a form, post a message, or add items to a database.</p>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Yes</td>
    </tr>
    <tr>
      <td style="text-align:left">DELETE</td>
      <td style="text-align:left">
        <p>Requests server removal of a specified resource.</p>
        <p>It is up to the server to archive or actually delete information.</p>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">No</td>
    </tr>
  </tbody>
</table>



