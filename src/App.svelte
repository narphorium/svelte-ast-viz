<script>
	import Tree from './Tree.svelte'
	let data = {
		type: 'module',
		expanded: false,
		children: [
			{ type: 'import_statement',
			expanded: false,
			  slots: {
					name: { type: 'aliased_import',
							expanded: false,
							slots: {
								name: 
									{ type: 'dotted_name',
									  expanded: false,
									  children: [{ type: 'identifier' }]},
								alias: { type: 'identifier' }
							}
					}
			  }
			},
			{ type: 'function_definition',
			  expanded: false,
			  slots: {
				name: { type: 'identifier' },
				parameters: { type: 'parameters' },
				body: 
					{ type: 'block', 
					  expanded: false,
					  children: [
						  { type: 'return_statement',
						    expanded: false,
						    children: [{ type: 'true' }]}]
				}
			  }
			},
			{ type: 'function_definition',
			  expanded: false,
			  slots: {
				name: { type: 'identifier' },
				parameters: { type: 'parameters',
							  expanded: false,
				              children: [{ type: 'identifier' }]},
				body: 
					{ type: 'block',
					  expanded: false,
					  children: [
							{ type: 'expression_statement',
							  expanded: false,
							  children: [{ type: 'string'}]},
							{ type: 'if_statement',
							  expanded: false,
							  slots: {
									condition: { type: 'identifier' }, 
									consequence: 
										{ type: 'block',
										  expanded: false,
										  children: [
											{ type: 'expression_statement',
											  expanded: false,
											  children: [
												{ type: 'call',
												  expanded: false,
												  slots: {
													function: { type: 'identifier' },
													arguments: { type: 'argument_list' }
												  }
												}
											  ]
											}
										  ]
										}
									}
								}
							]
					}
			  }
			},
			{ type: 'comment'}
		]
	}
</script>

<Tree {data} />

<link rel="stylesheet" href="tree.css" />
<style>
	:global(body) {
	margin: 0 0;
	}
</style>