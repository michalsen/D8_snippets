

Various snippets to reuse in this Drupal 8 adventure

```

use Drupal\views\ViewExecutable;

/**
 *  Implements hook_views_pre_render()
 *  Distinct Results
 *
 */
function MODULE_views_pre_render(ViewExecutable $view) {
  if ($view->id() == 'filter_manufacturer') {
    $manufacturers = [];
    $new_result = [];
       foreach($view->result as $k => $row) {
        if (!in_array($row->node__field_manufacturer_field_manufacturer_value, $manufacturers)) {
          $manufacturers[] = $row->node__field_manufacturer_field_manufacturer_value;
          $new_result[] = $row;
        }
       }
   $view->result = $new_result;
  }
}


Bulk delete command line using drush scr

use Drupal\Core\DrupalKernel;
use Drupal\Core\Site\Settings;

$autoloader = require_once __DIR__ . '/autoload.php';

$nodes = \Drupal::entityTypeManager()->getStorage('node')->loadMultiple($nids);

foreach ($nodes as $key => $node) {
  $type = $node->getType();
  if ($type == 'CONTENT_TYPE') {
    print $node->delete() . ".";
  }
}
