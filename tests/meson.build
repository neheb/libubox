tests = {
  'avl': [],
  'b64': [],
#  'b64_decode': [],
#  'b64_encode': [],
  'blob-buflen': [],
  'blobmsg': [json_script_dep],
  'blobmsg_check_array': [],
#  'blobmsg-parse': [],
#  'blobmsg-procd-instance': [],
  'blobmsg-types': [json_script_dep],
#  'blob-parse': [],
#  'json-script': [json_dep, json_script_dep],
  'list': [],
  'runqueue': [],
}

foreach t, d : tests
  test(t,
    executable(
      t,
      'test-@0@.c'.format(t),
      dependencies: [libubox_dep, blobmsg_json_dep, d]
    ),
  )
endforeach
