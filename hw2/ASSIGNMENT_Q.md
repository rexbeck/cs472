The Class Information Protocol and Course Registration Protocol could have matching PDU. The header values would be:
- Prototype Type (unchanged)
- Prototype Version (unchanged)
- Command: Would have more options than just class info. These options would include registration, override request, drop request.
- Direction (unchanged)
- Term (unchanged)
- Course (unchanged)
- Sections: This would be empty for sending the CIP request and would be populated with a list on response. A CRP request and response would have the wanted section.
- Pre-Requisites: Value is returned on CIP response or CRP response as an error. Otherwise NULL.
- Co-Requisites: Value is returned on CIP response or CRP response as an error. Otherwise NULL.
- Restrictions: Value is returned on CIP response or CRP response as an error. Otherwise NULL.
- Class Size: Value is returned on response, NULL for request.
- Enrolled: Value is returned on CIP response or CRP response as an error. Otherwise NULL.
- Authorization: NULL for CIP request/response as that is publically available information. Would require a bearer token that connects to student account, allowing server-side validations and sensitive information to stay private.

I believe building off the existing Class Information Protocol is the best course of action. Firstly, it already contained information that would be needed for the Course Registration Protocol, making building off it easy. Secondly, there is much overlap over what information is required to register for a course and what information could be given to someone asking. What overlap is not needed can easily be left NULL (like with authorization.)

The server would handle request validations, going through different flows depending on the command type as these commands would have different validations and required values. But the server would build different responses depending on what request was received.
