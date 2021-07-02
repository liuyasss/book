### Flutter widget

- Widget build 方法调用链

  ```
  main	#	runApp
  WidgetsBinding	#	scheduleAttachRootWidget
  WidgetsBinding	#	attachRootWidget
  RenderObjectToWidgetElement	#	mount
  RenderObjectToWidgetElement	#	_rebuild
  Element	#	updateChild
  Element	#	inflateWidget
  Element	#	mount
  ComponentElement	#	rebuild
  ComponentElement	#	performRebuild
  // StatefulElement 或者	StatelessElement
  StatefulElement	#	build	||	StatelessElement	# build
  State	#	build
  ```

  

> State#build
>
> StatefulElement#build<----ComponentElement#performRebuild <----ComponentElement#rebuild<----Element#mount<---- Element#inflateWidget<----Element#updateChild<----RenderObjectToWidgetElement#_rebuild



> ```
> StatefulWidget#createElement <----Widget#createElement <----Element#inflateWidget
> ```

- setState

  >
  >
  >Element#setState---->Element#markNeedBuild---->BuildOwner#scheduleBuildFor



