# Copyright 2011, The Toft Authors.

proto_library(
    name = 'rpc_option_proto',
    srcs = 'rpc_option.proto'
)

proto_library(
    name = 'rpc_message_proto',
    srcs = 'rpc_message.proto',
    deps = ':rpc_option_proto'
)

proto_library(
    name = 'rpc_meta_info_proto',
    srcs = 'rpc_meta_info.proto',
    deps = ':rpc_option_proto'
)

proto_library(
    name = 'rpc_error_code_info_proto',
    srcs = 'rpc_error_code_info.proto'
)

proto_library(
    name = 'rpc_builtin_service_proto',
    srcs = 'rpc_builtin_service.proto',
    deps = [
        ':rpc_option_proto',
        ':rpc_message_proto'
    ]
)

proto_library(
    name = 'rpc_channel_option_info_proto',
    srcs = 'rpc_channel_option_info.proto'
)

proto_library(
    name = 'rpc_client_option_info_proto',
    srcs = 'rpc_client_option_info.proto'
)

proto_library(
    name = 'rpc_server_option_info_proto',
    srcs = 'rpc_server_option_info.proto'
)

resource_library(
    name = 'static_resource',
    srcs = [
        'static/favicon.ico',
        'static/flags.html',
        'static/forms.html',
        'static/forms.js',
        'static/flags.js',
        'static/jquery-1.4.2.min.js',
        'static/jquery.json-2.2.min.js',
        'static/methods.html',
        'static/poppy.html',
        'static/status.html'
    ]
)

cc_library(
    name = 'poppy',
    srcs = [
        'rpc_builtin_service.cc',
        'rpc_channel.cc',
        'rpc_channel_impl.cc',
        'rpc_client.cc',
        'rpc_client_impl.cc',
        'rpc_connection.cc',
        'rpc_controller.cc',
        'rpc_error_code.cc',
        'rpc_form.cc',
        'rpc_handler.cc',
        'rpc_http_channel.cc',
        'rpc_request_queue.cc',
        'rpc_server.cc',
        'rpc_server_session_pool.cc',
        'rpc_text.cc',
        'stats_registry.cc'
    ],
    deps = [
        ':rpc_builtin_service_proto',
        ':rpc_channel_option_info_proto',
        ':rpc_client_option_info_proto',
        ':rpc_error_code_info_proto',
        ':rpc_meta_info_proto',
        ':rpc_server_option_info_proto',
        ':static_resource',
        '//toft/base:binary_version',
        '//toft/base:export_variable',
        '//toft/base/string:string',
        '//toft/crypto/credential:credential',
        '//toft/crypto/hash:hash',
        '//toft/crypto/random:random',
        '//toft/encoding:encoding',
        '//toft/net/http:http',
        '//toft/net/uri:url',
        '//toft/netframe:netframe',
        '//toft/system/cpu:cpu',
        '//toft/system/io:io',
        '//toft/system/memory:memory',
        '//toft/system/net:domain_resolver',
        '//toft/system/timer:timer',
        '//poppy/address_resolver:address_resolver',
        '//thirdparty/ctemplate:ctemplate',
        '//thirdparty/perftools:profiler',
        '//thirdparty/snappy:snappy',
        '//thirdparty/jsoncpp:jsoncpp',
    ]
    # defs = [
    #     'LIST_TODO'
    # ]
)

cc_library(
    name = 'poppy_mock',
    srcs = [
        'rpc_mock.cc',
        'rpc_mock_channel.cc',
        'rpc_mock_channel_impl.cc',
    ],
    deps = [
        ':poppy',
        '//toft/base:module',
        '//toft/protobuf_extensions:protobuf_extensions',
        '//thirdparty/gmock:gmock'
    ],
    link_all_symbols = 1,
)

cc_library(
    name = 'poppy_swig_wrap',
    srcs = 'rpc_channel_swig.cc',
    deps = ':poppy'
)

cc_test(
    name = 'rpc_channel_test',
    srcs = 'rpc_channel_test.cc',
    deps = '//poppy:poppy'
)

cc_test(
    name = 'rpc_client_test',
    srcs = 'rpc_client_test.cc',
    deps = '//poppy:poppy'
)

cc_test(
    name = 'rpc_controller_test',
    srcs = 'rpc_controller_test.cc',
    deps = '//poppy:poppy'
)

cc_test(
    name = 'rpc_form_test',
    srcs = 'rpc_form_test.cc',
    deps = [
        '//poppy:poppy',
        '//thirdparty/perftools:tcmalloc',
        '//thirdparty/gtest:gtest'
    ]
)

#"""
# Don't delete this block. It's for python/java version poppy client.
# We comments them out just because most users don't need them, even
# some dev machine even don't have jdk installed.
swig_library(
    name = 'poppy_client',
    srcs = 'poppy_client.i',
    deps = ':poppy_swig_wrap',
    warning = 'yes',
    java_lib_packed = 'yes',
    java_package = 'com.soso.poppy.swig'
)
#"""

