
#this can be used to update the entry symbol to use
set(EXTENSION_ENTRY_SYMBOL "GDExtensionInit")

add_library(${EXTENSION_NAME} SHARED)

target_compile_features(${EXTENSION_NAME} PRIVATE cxx_std_17)

target_sources(${EXTENSION_NAME} PRIVATE
    src/RegisterExtension.cpp
)

set_target_properties(${EXTENSION_NAME} PROPERTIES
    DEBUG_POSTFIX "-d"
)

add_custom_command(TARGET ${EXTENSION_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory $<TARGET_FILE_DIR:${EXTENSION_NAME}> ${OUTPUT_DIR}
)

target_link_libraries(${EXTENSION_NAME} PUBLIC godot-cpp)

#create our gdextension file
#get the formatting right on for hot reload
if(EXTENSION_HOT_RELOADABLE)
    set(HOT_RELOAD "true")
else()
    set(HOT_RELOAD "false")
endif()

configure_file("gdextension.in" "${GODOT_PROJECT_DIR}/${EXTENSION_NAME}.gdextension")

unset(HOT_RELOAD)
