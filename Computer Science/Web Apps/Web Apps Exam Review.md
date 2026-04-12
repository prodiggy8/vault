Uniform Resource Locator (URL) or  Uniform Resource Identifier (URI)
- protocol://dns-name:port/identifier
- scheme://domain:port/path?query#id

**Markup languages:** describe how to **structure and present a document**
**Hyper-text Markup Language (HTML)**
- Documents contain markup and content
- **Elements:** start and end tags and everything in between
- Attributes specified in a start tag

**HTML5:** more consistent, more tags (article, figure, section, time, new input types, graphics, media)
	<div\> breaks lines
	<span\> is "in" the current text line
	They do nothing but allow CSS to be specified
**CSS:** to separate presentation from content
	.selector for classes (not unique and many allowed)
	\#selector for IDs (unique and only one)
	element.class (can recurse)
	.parent { .child {} } (can nest)
	Pseudo-classes: :hover, :focus, :first-child, etc
	**Hierarchical!**
		1. ID
		2. Class
		3. Element
	**Margin** is space around an element, outside of its border
	**Padding** is space between element's content and border
	
![[Pasted image 20260210145206.png]]

**DOM:** object model for an HTML document
- Bridge between JS and HTML/CSS
- Browser parses HTML and creates a tree
**JavaScript:** browser-based (native) scripting language
- Full-stack (Node.js)
- Largest ecosystem
- Async by default

**AJAX:** allows asynchronous HTTP calls

**HTTP & Django:**
Hyper-text Transfer Protocol
- GET and POST (others but not used in web)
- GET path HTTP/1.1 ... \n
	- Connection: keep-alive (default) - keeps socket open
	- Parameters send in query string
- POST: Content-Length & Content-Type and then the message body
	- Parameters send in request body

200 - OK
3xx - "detours" (moved, etc)
4xx - User error (bad request, unauthorized, forbidden, not found)
5xx - Internal Server Error

**Django**
- Project folder & apps folders
- app/static/app -> static files (CSS, JS, static HTML)
- app/templates/app -> Django templates

Uses MVC:
- Views/URLs (controller)
- Models (model)
- Templates (view)

#### Hidden fields, cookies, and sessions (state management)

Hidden fields
- Must always validate data (user can change)
- Requires no browser storage or server side memory
- Sent back and forth
- "Back button problem" will send fields again! Requires idempotency.

Cookies
- Browser's Key-Value Store
- HTTP Header Level
	- Cookie/Set-Cookie fields
- Server sends browser in HTTP response
- Browser sends them back in subsequent requests
- Attributes:
	- Expires (datetime), max-age (timestamp), domain, path, secure (SSL), HTTPOnly, SameSite (don't send on requests from pages originated from other sites)
- Can be modified by user
- Limited (50 per domain, 3k max in browsers)
- GDPR: must notify users, allow opt-out

Sessions
- Maintain data correlated with browser session
- Session cookie: without max-age or expires attribute; deleted when session ends.
- Persistent cookie - stored until expiration date
- Third party cookie: ads/images etc, used for tracking


XSS: injecting scripts/HTML in site's data, e.g., put HTML/JS in a to-do list
CSRF: Site A tricks user into submitting request to Site B
- SameSite prevents this
- Setting CSRF tokens on incoming POST requests
- Not used in GET because that's the function of get (linking to other sites)
- Django: request must include a hidden field called csrfmiddlewaretoken

**All tabs share same cookies, and hence sessions**

#### Responsive Web Design (RWD)

- Scaling appropriately on different devices
- Mobile specific websites on the past, e.g., m.google.com.
- WURLF and RESS (server-side detection)

Adaptive: generate templates optimize for a **unique device class**
Responsive: universal design that reflows across displays

Viewports: **visible area of a webpage on a device**
- often not the same as the size of the device

Apple invented:
`<meta name="viewport" content="width=device-width, initial-scale=1.0"`

px in CSS is **different from device pixels**. Initial scale sets zoom to 1 CSS pixel equal to 1 device pixel.

Relative units:
- em (element font size)
- rem (root font size)
- % (relative to parent element)
- vw (percent of viewport width)
- vh (percent of viewport height)

**Media queries:** specify breakpoints for min/max viewport sizes
- `@media screen and (max-width: 768px) { background-color: darkgreen; }`

**Flexbox:**
- Layout option for flexible arrangement
- `display: flex`
- Specify **alignment and distribution of elements in container**
- If enough space, elems **stay in row**, otherwise **shrink** (`flex-wrap: nowrap`) or wrap to **next line**

**Grid**
- Used for structured layouts (photo galleries, dashboards, etc)
- Specify number and size of columns and rows

**UI frameworks:** takes the hassle out of CSS
- Bootstrap, Tailwind, React

#### Forms

`forms.Form` superclass
`forms.CharField`
`forms.IntegerField`
`forms.DateField`

`{{ form }}` to generate in template (need to set in context `views.py`)
**Return** with `render(request, template, context)`

- Superclass contains validation (`is_valid()`)
- Contains cleaned data (`cleaned_data[field]`)

Uses browser validation as well when rendering: required fields, numeric input, date values, email and URL. But all of that is **done again in the server side**!

**Templates**

- Creating redundant folders with application name prevents Django from conflicting files with same name as it looks up for templates in the `templates` folders.
- Template inheritance

In `base.html`:
```
<div class="content"> {% block content %} {% endblock %} </div>
```

In `child.html`:
```
{% block content %} <h1>Welcome to the Homepage!</h1> <p>This unique text lives inside the base skeleton.</p> {% endblock %}
```

Formatting forms:
```
{{ form.as_p }}
{{ form.as_table }}
{{ form.as_div }}
```

- Declaring names in `urls.py` to be able to use `{% url %}`
- Declaring URL parameters `path('edit/<int:id>', views.action)`
#### Authentication

- Field specific clean functions in forms, `clean_fieldname()`
- Can override the `clean()` of superclass
- `django.contrib.auth` system!
	- `create_user()`
	- `authenticate()`
	- `login()`
	- `redirect()`
	- `@login_required` decorator
	- `LOGIN_URL` and `LOGIN_REDIRECT_URL` in `settings.py`
	- The example uses `/oauth/login/google-oauth2/`

Salt and hash passwords!

**OAuth** is an open authentication protocol
Permits applications to use another site's authentication services

#### Models

- ORM: writing queries for everything is hard!
- Superclass `django.db.models.Model`
- `models.ForeignKey(User,...)` many-to-one relationship
- `on_delete` behavior
	- `models.PROTECT` prevents deletion if related object exists
	- `models.CASCADE` deletes related objects
- `request.user.email.endswith("andrew.cmu.edu")`
- 

