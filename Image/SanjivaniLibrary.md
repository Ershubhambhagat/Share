#Single Button Example

NEXT_PUBLIC_FLOATING_BUTTONS=[{"id":"agentai","url":"https://agent.ai/chat","image":"https://cdn.example.com/ai-icon.png","label":"Agent AI"}]

#Multiple Buttons Example

NEXT_PUBLIC_FLOATING_BUTTONS=[{"id":"agentai","url":"https://agent.ai","image":"https://i.imgur.com/abc123.png","label":"Agent AI","order":1},{"id":"support","url":"https://support.com","image":"https://i.imgur.com/xyz789.png","label":"Help","order":2,"visibleOn":["student"]}]

#Full Configuration Example (all options)


NEXT_PUBLIC_FLOATING_BUTTONS=[{"id":"agentai","url":"https://agent.ai","image":"https://your-image-url.png","label":"Agent AI","enabled":true,"position":"bottom-right","size":50,"target":"_blank","order":1,"style":"round","visibleOn":["student","admin"],"bgColor":"bg-gradient-to-br from-purple-400 to-purple-600"}]
Quick Reference
Property	Required	Example Values
id	Yes	"agentai"
url	Yes	"https://agent.ai"
image	Yes	"https://cdn.com/icon.png"
label	No	"Agent AI"
enabled	No	true / false
position	No	"bottom-right", "bottom-left", "top-right", "top-left"
size	No	50 (pixels)
target	No	"_blank" (new tab), "_self" (same tab)
order	No	1, 2, 3... (stacking order)
visibleOn	No	["student"], ["admin"], ["student","admin"]
Just paste the JSON in Vercel's environment variables section for NEXT_PUBLIC_FLOATING_BUTTONS
