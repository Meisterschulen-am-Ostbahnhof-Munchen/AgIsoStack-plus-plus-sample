# This component demonstrates how to add an existing third-party library as a component
# to ESP-IDF build system.
#
# Since we are wrapping the library inside a component,
# the component has to be registered first:
idf_component_register()


include_directories(${IDF_PATH}/components/driver/twai/include)
include_directories(${IDF_PATH}/components/driver/gpio/include)
include_directories(${IDF_PATH}/components/pthread/include)


# Set CAN_DRIVER to TWAI, as we are on ESP32
set(CAN_DRIVER "TWAI")

# A handy function to prepend text to all elements in a list (useful for
# subdirectories)
function(prepend var prefix)
  set(listVar "")
  foreach(arg ${ARGN})
    list(APPEND listVar "${prefix}/${arg}")
  endforeach(arg)
  set(${var}
      "${listVar}"
      PARENT_SCOPE)
endfunction(prepend)

# Add subdirectories
add_subdirectory("isobus/utility")
add_subdirectory("isobus/isobus")
add_subdirectory("isobus/hardware_integration")


target_link_libraries(${COMPONENT_LIB} INTERFACE Isobus HardwareIntegration Utility)