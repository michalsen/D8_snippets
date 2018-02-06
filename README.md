



```

/**
 *  Implements hook_views_pre_render()
 *  Distinct Results
 *
 *  use Drupal\views\ViewExecutable;
 */
function cncex_views_views_pre_render(ViewExecutable $view) {
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
