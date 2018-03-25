# WordPress API in OOP way.

## WordPress API
### Settings API
Allows admin pages containing settings forms to be managed semi-automatically. It lets you define settings pages, sections within those pages and fields within the sections. [More](https://codex.wordpress.org/Settings_API)
### Options API
A simple and standardized way of storing data in the database. The API makes it easy to create, access, update, and delete options. All the data is stored in the wp_options table under a given custom name. [More](https://codex.wordpress.org/Options_API)
### Widgets API
Widgets were originally designed to provide a simple and easy-to-use way of giving design and structure control of the WordPress Theme to the user, which is now available on properly "widgetized" WordPress Themes to include the header, footer, and elsewhere in the WordPress design and structure. [More](https://codex.wordpress.org/Widgets_API)

## Current usage
```php
use NWP\Menu;
use NWP\SubMenu;

/**
 * Create custom admin menu and submenu
 */
// Create menu and submenu
$menu = new Menu( 'NWP Menu', 'nwp-menu', 'manage_options', function() {
	echo 'NWP Custom Menu';
});
$submenu = new SubMenu( 'NWP Submenu', 'nwp-submenu', 'manage_options', function() {
	echo 'NWP Custom Submenu';
});

// Add CSS and JS to submenu (menu can do this as well)
$submenu->addStyle( 'my-submenu-css', get_stylesheet_directory_uri() . '/inc/admin.css' )
		->addScript( 'my-submenu-js', get_stylesheet_directory_uri() . '/inc/admin.js' );

// Add submenu
$menu->addSub( $submenu )
	 ->create();

// Hide top level menu
Menu::hide( ['themes.php', 'edit.php'] );
// Hide submenu using slug
Menu::hide( 'nwp-menu', 'nwp-submenu' );
// Hide submenu using Submenu instance
Menu::hide( $my_menu, $my_submenu );
```

### Future usage
```php
use NWP\Widget;

$widget = new Widget( 'widget_id', 'Widget Name', 'Widget description');

$widget->addWidgetCallback( 'user_widget_callback' )
	   ->addFormCallback( 'user_form_callback' )
	   ->addUpdateCallback( 'user_update_callback' );
	   ->create();

function user_widget_callback() { /* content of widget on frontend page here */ }
function user_form_callback() { /* form of widget on admin page here */ }
function user_update_callback() { /* update widget setting here */ }
```

### The widget API above is currently unavailable due to the bug I still haven't found a way to fix it yet. :(