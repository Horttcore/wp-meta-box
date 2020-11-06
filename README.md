# WordPress Meta Box Helper

## Installation

`$ composer require ralfhortt/wp-meta-box`

## Usage

* Extend `RalfHortt\MetaBoxes\MetaBox()`
* You _MUST_ set `$this->identifier`, `$this->name`, `$this->screen` in the class constructor
* You _CAN_ set the additional variables `$this->context`, `$this->priority`, `$this->callbackArgs`
* Add a `render()` method
* Add a `save()` method
* A nonce is added automatically and checked

## Example

```php
<?php
use RalfHortt\MetaBoxes\MetaBox;

class MyMetaBox extends MetaBox
{
	protected $identifier = 'my-meta-box';
	protected $name = 'My Meta Box';
	protected $screen = ['post'];
	protected $context = 'side';
	protected $priority = 'high';

	function render(\WP_Post $post): void 
	{
		?>
		<label for="my-meta">Meta Label</label>
		<input id="my-meta" name="my-meta" class="regular-text" type="text" value="<?= esc_attr(get_post_meta($post->ID, 'my-meta', true )) ?>">
		<?php
	}

	function save(int $postId, \WP_Post $post, bool $update): void
	{
		update_post_meta($postId, 'my-meta', sanitize_text_field($_POST['my-meta']));
	}
}
```

## Changelog

### v1.1.0

* Add save_post args

### v1.0.0

* Initial release
