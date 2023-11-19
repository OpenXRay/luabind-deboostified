add_library(xrLuabindApi INTERFACE)

# API headers
target_sources(xrLuabindApi INTERFACE
    back_reference.hpp
    back_reference_fwd.hpp
    class.hpp
    class_info.hpp
    config.hpp
    error.hpp
    error_callback_fun.hpp
    exception_handler.hpp
    from_stack.hpp
    function.hpp
    function_introspection.hpp
    get_main_thread.hpp
    handle.hpp
    lua_argument_proxy.hpp
    lua_extensions.hpp
    lua_include.hpp
    lua_index_proxy.hpp
    lua_iterator_proxy.hpp
    lua_proxy.hpp
    lua_proxy_interface.hpp
    lua_state_fwd.hpp
    luabind.hpp
    make_function.hpp
    memory.hpp
    memory_allocator.hpp
    nil.hpp
    no_dependency.hpp
    object.hpp
    open.hpp
    operator.hpp
    pointer_traits.hpp
    prefix.hpp
    scope.hpp
    set_package_preload.hpp
    shared_ptr_converter.hpp
    typeid.hpp
    types.hpp
    version.hpp
    weak_ref.hpp
    wrapper_base.hpp
)

# Detail API headers
target_sources(xrLuabindApi INTERFACE
    detail/call.hpp
    detail/call_function.hpp
    detail/call_member.hpp
    detail/call_shared.hpp
    detail/call_traits.hpp
    detail/class_registry.hpp
    detail/class_rep.hpp
    detail/constructor.hpp
    detail/conversion_storage.hpp
    detail/crtp_iterator.hpp
    detail/debug.hpp
    detail/decorate_type.hpp
    detail/deduce_signature.hpp
    detail/enum_maker.hpp
    detail/format_signature.hpp
    detail/garbage_collector.hpp
    detail/inheritance.hpp
    detail/instance_holder.hpp
    detail/link_compatibility.hpp
    detail/make_instance.hpp
    detail/meta.hpp
    detail/object.hpp
    detail/object_rep.hpp
    detail/open.hpp
    detail/operator_id.hpp
    detail/other.hpp
    detail/pcall.hpp
    detail/policy.hpp
    detail/primitives.hpp
    detail/property.hpp
    detail/ref.hpp
    detail/signature_match.hpp
    detail/stack_utils.hpp
)

# Default policies headers
target_sources(xrLuabindApi INTERFACE
    detail/conversion_policies/conversion_base.hpp
    detail/conversion_policies/conversion_policies.hpp
    detail/conversion_policies/enum_converter.hpp
    detail/conversion_policies/function_converter.hpp
    detail/conversion_policies/lua_proxy_converter.hpp
    detail/conversion_policies/native_converter.hpp
    detail/conversion_policies/pointer_converter.hpp
    detail/conversion_policies/reference_converter.hpp
    detail/conversion_policies/value_converter.hpp
)

# User policies headers
target_sources(xrLuabindApi INTERFACE
    adopt_policy.hpp
    container_policy.hpp
    copy_policy.hpp
    dependency_policy.hpp
    discard_result_policy.hpp
    iterator_policy.hpp
    out_value_policy.hpp
    raw_policy.hpp
    return_reference_to_policy.hpp
    yield_policy.hpp
)

target_include_directories(xrLuabindApi
    INTERFACE
    "${CMAKE_CURRENT_SOURCE_DIR}/.."
)
