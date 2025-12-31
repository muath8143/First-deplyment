<!-- README.html (You can paste this directly into GitHub README.md — GitHub renders HTML) -->

<h1>Sijal (سِجال) – AI Interview Preparation Platform</h1>

<hr />

<h2>نبذة عن المشروع (بالعربي)</h2>
<p>
<strong>سِجال</strong> منصة تساعد المستخدم على الاستعداد للمقابلات الوظيفية عبر جلسات مقابلة صوتية،
حيث يتم إنشاء جلسة مقابلة وتوليد أسئلة مخصصة (حسب السيرة الذاتية أو الوصف الوظيفي)،
ثم يتم حفظ التسجيل والنص (Transcript) وتحليل الإجابات باستخدام الذكاء الاصطناعي لإعطاء تقييم ونقاط قوة/ضعف.
</p>

<h2>Project Overview (English)</h2>
<p>
<strong>Sijal</strong> is an AI-powered interview preparation platform that enables users to run voice-based mock interviews.
The system creates an interview session, generates tailored questions (from CV and/or job description),
collects call artifacts (recording + transcript), and produces AI-driven feedback including a final score,
strengths, and weaknesses.
</p>

<hr />

<h2>Team</h2>
<ul>
  <li>Muath</li>
  <li>Jumana</li>
  <li>Abdulmajid</li>
</ul>
<p>
<strong>Note:</strong> Database relationships/ERD were designed collaboratively by the whole team (not attributed to one person).
</p>

<hr />

<h2>Core Features</h2>
<ul>
  <li>Create interview sessions and generate questions based on CV and/or job description</li>
  <li>Voice interview simulation (phone call) with session validation</li>
  <li>Store interview recording and transcript after call ends</li>
  <li>AI interview analysis (final score + strengths + weaknesses)</li>
  <li><strong>HR Interview module:</strong> conduct interviews with HR and store HR evaluation</li>
  <li><strong>AI Improvement Plan:</strong> generate a personalized development plan for the user based on feedback</li>
  <li>Retrieve user sessions and session details with authorization (ownership checks)</li>
  <li>Health endpoint for deployment monitoring</li>
</ul>

<hr />

<h2>Muath’s Contributions</h2>
<ul>
  <li>Implemented Interview Session flow endpoints (start session, get sessions, get session by id, get questions payload)</li>
  <li>Implemented AI Analysis retrieval endpoints (per customer / per session with ownership check)</li>
  <li>Implemented Vapi webhook endpoint integration for handling end-of-call artifacts</li>
  <li>Implemented Questions endpoints (add/get/questions-for-session with authorization)</li>
  <li>Implemented a simple Health endpoint for environment checks</li>
  <li>
    Implemented OpenAI integration method:
    <ul>
      <li><code>OpenAiService.ask(prompt)</code> (only)</li>
    </ul>
  </li>
</ul>

<hr />

<h2>API Endpoints (Muath)</h2>

<h3>Health</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><code>/health</code></td>
      <td>Server health check</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

<h3>Interview Sessions</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/interview-session/start-session-with-cv</code></td>
      <td>Create a session and generate questions using CV</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/interview-session/start-session-with-description</code></td>
      <td>Create a session and generate questions using job description</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/interview-session/get_question/{sessionId}</code></td>
      <td>Public payload for voice agent (valid + questions)</td>
      <td>No</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/interview-session/get-my-sessions</code></td>
      <td>Get all sessions for the authenticated user</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/interview-session/get-session-by-id/{sessionId}</code></td>
      <td>Get session details by id (ownership enforced)</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Questions</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/questions/add</code></td>
      <td>Add a question</td>
      <td>(Project rules)</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/questions/get-all</code></td>
      <td>Get all questions</td>
      <td>(Project rules)</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/questions/questions-for-session/{sessionId}</code></td>
      <td>Get questions for a session (ownership enforced)</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>AI Analysis</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/analysis-by-ai/all-analysis</code></td>
      <td>Get all analyses for authenticated user sessions</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/analysis-by-ai/analysis-for-session/{sessionId}</code></td>
      <td>Get analysis for a specific session (ownership enforced)</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Vapi Webhook</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/vapi/webhook</code></td>
      <td>Receive end-of-call report and process recording/transcript</td>
      <td>No (secured by webhook secret recommended)</td>
    </tr>
  </tbody>
</table>

<hr />

<h2>Jumana’s Contributions</h2>
<ul>
  <li>Implemented HR management module (register/update/delete/activate HR + ordered listing)</li>
  <li>Implemented HR interview lifecycle (start/update/cancel/end/delete + retrieval for customer/HR)</li>
  <li>Implemented HR analysis module (CRUD interview analysis + development plan endpoint)</li>
  <li>Implemented HR rating module (add/update/delete + top rating + filters by HR/customer)</li>
  <li>Implemented interview request module (send/update/approve/reject/delete + list requests)</li>
  <li>Implemented subscription module (subscribe/get/cancel)</li>
  <li>Implemented payment status & callback endpoints</li>
  <li>Implemented card management endpoints (add/update/delete + get cards + get my cards)</li>
  <li>Implemented Jitsi meeting link creation service</li>
  <li>Implemented email service (basic email + attachments and CV sending)</li>
</ul>

<hr />

<h2>API Endpoints (Jumana)</h2>

<h3>HR Management</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/hr/register-hr</code></td>
      <td>Register HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/hr/update-hr</code></td>
      <td>Update HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/hr/delete-hr</code></td>
      <td>Delete HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/hr/activate-hr/{hr_id}</code></td>
      <td>Activate HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/hr/get-hr</code></td>
      <td>Get HR list</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/hr/get-hr-ordered</code></td>
      <td>Get ordered HR list</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Interview With HR</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/Interview-with-hr/start-interview/{interview_id}</code></td>
      <td>Start HR interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/Interview-with-hr/update-interview/{interview_id}</code></td>
      <td>Update HR interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/Interview-with-hr/cancel-interview/{interview_id}</code></td>
      <td>Cancel HR interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/Interview-with-hr/end-interview/{interview_id}</code></td>
      <td>End HR interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/Interview-with-hr/delete-interview/{interview_id}</code></td>
      <td>Delete HR interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-with-hr/get-interviews</code></td>
      <td>Get all HR interviews</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-with-hr/get-interview-by-customer</code></td>
      <td>Get HR interviews for customer</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-with-hr/get-interview-by-hr</code></td>
      <td>Get HR interviews for HR</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Interview Analysis By HR</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/Interview-analysis-by-hr/add-interview-analysis/{interview_id}</code></td>
      <td>Add interview analysis (HR evaluation) for an interview</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/Interview-analysis-by-hr/update-interview-analysis/{analysis_id}</code></td>
      <td>Update interview analysis</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/Interview-analysis-by-hr/delete-interview-analysis/{analysis_id}</code></td>
      <td>Delete interview analysis</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-analysis-by-hr/get-interviews-analysis</code></td>
      <td>Get all interviews analysis</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-analysis-by-hr/get-interview-analysis-by-customer</code></td>
      <td>Get analysis by customer</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-analysis-by-hr/get-interview-analysis-by-hr</code></td>
      <td>Get analysis by HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/Interview-analysis-by-hr/development-plan</code></td>
      <td>Get development plan (improvement plan) for customer</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>HR Rating</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/rating-hr/add-rating/{hr_id}</code></td>
      <td>Add rating for HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/rating-hr/update-rating{rating_id}</code></td>
      <td>Update rating</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/rating-hr/delete-rating/{rating_id}</code></td>
      <td>Delete rating</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/rating-hr/get-rating</code></td>
      <td>Get all ratings</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/rating-hr/get-top-rating</code></td>
      <td>Get top rated HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/rating-hr/get-rating-by-hr/{hr_id}</code></td>
      <td>Get ratings for a specific HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/rating-hr/get-rating-by-customer</code></td>
      <td>Get ratings created by customer</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Request Interview</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/request-interview/send-request/{hr_id}</code></td>
      <td>Send interview request to HR</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/request-interview/update-request/{request_id}</code></td>
      <td>Update interview request</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/request-interview/approve-request/{request_id}</code></td>
      <td>Approve request</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/request-interview/reject-request/{request_id}</code></td>
      <td>Reject request</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/request-interview/delete-request/{request_id}</code></td>
      <td>Delete request</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/request-interview/get-request</code></td>
      <td>Get requests</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Subscription</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/subscription/subscribe</code></td>
      <td>Create subscription</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/subscription/get-subscription</code></td>
      <td>Get subscription</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/subscription/cancel-subscribe/{subscription_id}</code></td>
      <td>Cancel subscription</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Cards</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><code>/api/v1/card/add-card</code></td>
      <td>Add card</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PUT</td>
      <td><code>/api/v1/card/update-card/{card_id}</code></td>
      <td>Update card</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td><code>/api/v1/card/delete-card/{card_id}</code></td>
      <td>Delete card</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/card/get-cards</code></td>
      <td>Get all cards</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/card/get-my-cards</code></td>
      <td>Get my cards</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

<h3>Payments</h3>
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Endpoint</th>
      <th>Description</th>
      <th>Auth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/payments/get-status/{id}</code></td>
      <td>Get payment status</td>
      <td>No</td>
    </tr>
    <tr>
      <td>GET</td>
      <td><code>/api/v1/payments/callback</code></td>
      <td>Payment gateway callback</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

<hr />

<h2>Services (Muath)</h2>
<table>
  <thead>
    <tr>
      <th>Service</th>
      <th>Main Responsibility</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>InterviewSessionService</code></td>
      <td>Create session, generate questions, email session ID, return session payload, fetch user sessions</td>
    </tr>
    <tr>
      <td><code>QuestionService</code></td>
      <td>CRUD for questions + generate questions from CV / CV + job description</td>
    </tr>
    <tr>
      <td><code>RecordingInterviewService</code></td>
      <td>Handle Vapi webhook, store recording/transcript, trigger AI analysis</td>
    </tr>
    <tr>
      <td><code>InterviewAnalysisByAiService</code></td>
      <td>Return AI analysis DTOs (per user / per session) + save AI analysis for transcript</td>
    </tr>
    <tr>
      <td><code>OpenAiService</code></td>
      <td><strong>Muath contribution:</strong> <code>ask(prompt)</code> only</td>
    </tr>
  </tbody>
</table>

<hr />

<h2>Services (Jumana)</h2>
<table>
  <thead>
    <tr>
      <th>Service</th>
      <th>Main Responsibility</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>JitsiService</code></td>
      <td>Create Jitsi room link (meeting link generation)</td>
    </tr>
    <tr>
      <td><code>SendMailService</code></td>
      <td>Send emails (simple message + with attachment + CV sending)</td>
    </tr>
  </tbody>
</table>

<hr />

<h2>Links</h2>
<ul>
  <li><strong>ERD:</strong> <a href="PUT_ERD_LINK_HERE">PUT_ERD_LINK_HERE</a></li>
  <li><strong>Postman Documentation:</strong> <a href="https://documenter.getpostman.com/view/51095397/2sBXVbJZNn">https://documenter.getpostman.com/view/51095397/2sBXVbJZNn</a></li>
  <li><strong>Figma:</strong> <a href="PUT_FIGMA_LINK_HERE">PUT_FIGMA_LINK_HERE</a></li>
  <li><strong>Domain:</strong> <a href="https://sijal.tech">https://sijal.tech</a></li>
</ul>
