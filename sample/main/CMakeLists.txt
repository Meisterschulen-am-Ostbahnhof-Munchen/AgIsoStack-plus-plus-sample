idf_component_register(
	SRCS 
		"main.cpp" 
		"console_logger.cpp"
    INCLUDE_DIRS 
    	"." 
    	"include"
    	"../components/AgIsoStack-plus-plus/isobus/hardware_integration/include"
    	"../components/AgIsoStack-plus-plus/isobus/isobus/include"
    	"../components/AgIsoStack-plus-plus/isobus/utility/include"
    )


target_add_binary_data(${COMPONENT_TARGET} "object_pool/object_pool.iop" BINARY)
