# nodejs-twilio-voicemail

Twilio
+61 8 7078 7804

contact-inbound Slack channel
Webhook: https://hooks.slack.com/services/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


Test the Slack channel webhook:
curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' https://hooks.slack.com/services/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


Twilio incoming call webhook:
http://twimlets.com/voicemail?Email=contact%40mechanicalrock.io&Message='%20'&Transcribe=true&


For the lambda invocation in Connect both the Success and Error outflows must point to the Transfer-to-number action or the call will just hang up - the transfer will not occur.

Lambda (uses slack-lambda-layer):
const pts = require('posttoslack');
exports.handler = async(event, context) => {
    const selection=event.Details.ContactData.Attributes.Selection
    console.log("User selection: " + selection)
    const calling_number=event.Details.ContactData.CustomerEndpoint.Address
    console.log("Calling number: " + calling_number)
    return pts.posttoslack("hooks.slack.com", "/services/T66G01W5R/BM6QPS9U6/NLiT5uYMrf3T320DTf5P3L5Z", "@channel Call for " + selection + " from " + calling_number);
};
