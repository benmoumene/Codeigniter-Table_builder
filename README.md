# Codeigniter-Table_builder
Simple library for generating Boostrap 4 searchable, paginated tables in Codeigniter using base CI3 model and pagination classes.

## Usage 

1. Upload the Table_builder.php library to application/libraries
2. Either load in application/config/autoload.php or from a controller
3. Ready to use
4. OPTIONAL - If you'd like to use the search the other library https://github.com/KeithBradley/Codeigniter-Form_builder can help so add that.

Example:

~~~

// SEARCH
if ( $this->input->get('keyword') ) {
  $this->db->like('name', $this->input->get('keyword'));
}

$this->table_builder->setData($this->db->from('db_table_name'), array(
  'base_url' => site_url('search'),
  'per_page' => 10,
  // OTHER CI PAGINATION CONFIG ITEMS
));

$this->table_builder->setHeading('id');
$this->table_builder->setHeading('name', array(
  'label' => 'Some Name',
  'callback' => function($value, $row_id)
  {
    return anchor('item/' . $row_id, $value);
  }
));

// OPTIONAL SEARCH (Install step #4)
$this->table_builder->setSearchField(array(
  'type' => 'text',
  'input' => array(
	'name' => 'keyword',
	  'label' => 'Keyword...',
		'value' => $this->input->get('keyword')
	),
));

// THIS CAN ALSO BE CHAINED
$this->table_builder->setHeading('id')->setHeading('name');

// ON THE VIEW
$this->table_builder->generate();

~~~
