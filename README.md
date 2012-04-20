# CakePan - CakePHP Mustache Support (CakePHP v2.x)

CakePan is a CakePHP view helper that renders Mustache templates. It will also load and process sub-templates!

### Why use Mustache templates in CakePHP?
<strong>Portability and scalability!</strong> If you have an app that uses lots of front-end coding, you only have to write your templates once. Mustache templates can be rendered in PHP, Javascript, Ruby, Scala, even C++! If you want to move to or from some other framework (Rails, Grails, Lithium etc.), you can be sure that your views and design won't have to be re-built.

For scalability, when the time comes, you can use templates with a more powerful engine like Scala, or just send JSON from any source, and render with Javascript. 

## Installation

### 1. Add the [PHP Mustache library](https://github.com/bobthecow/mustache.php/) to `app/vendors/mustache`
### 2. Add CakePan's `MustacheHelper.php` file to `app/Views/Helpers`. 
### 3. Add the Mustache View Helper to your pages.

CakePan should be added to your project the same as any other CakePHP View Helper. See the [Cakebook's View Helpers documentation](http://book.cakephp.org/2.0/en/views/helpers.html) for more information.

If you want to add Mustache support globally, add it to your `AppController`

	class AppController extends Controller {
		...
		public $helpers = array('Mustache');
		...
	}

## Usage

See the Mustache manual: [http://mustache.github.com/](http://mustache.github.com/)

### Creating a Mustache Template

Your Mustache templates should all be in the `/app/View/Elements/` directory, with a `.mustache` extension.

/app/View/Elements/post.mustache

	{{#Post}}
	<h2>{{title}}</h2\>
	<div>
		{{text}}
	</div>
	{{/Post}}


### Rendering a Mustache Template

All the variable set by the controller are available, and merged with values passed into `$params`.

	$params = array(
		'title' => 'Show me the bacon!',
		'text' => 'Bacon ipsum dolor sit amet fatback pig swine...'
	);

	$this->Mustache->render('template_name', $params)



### Sub-templates

Sub-templates should follow the same naming convention. Mustache will pass the variables to the sub-template in the context that it's called. For example, a nested template for a blog `post` with `comments` might look like:

/app/View/Elements/posts/post.mustache:

	{{#Post}}
	<h2>{{title}}</h2\>
	<div>
		{{text}}
	</div>
	{{/Post}}
	{{#Comment}}
		{{>post/comment}}
	{{/Comment}}

/app/View/Elements/posts/comment.mustache:

	<div>
	<h3>{{#User}}{{name}}{{/User}} said: </h3>
	<p>{{text}}</p>
	</div>