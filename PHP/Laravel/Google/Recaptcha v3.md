```
@extends('web.layouts.master')
@section('content')
<section id="screenshot" class="bgc-one-top mts-custom-sec mts-section-wrapper mts-description ">
   <div class="container sec-contact">
      <div class="row">
         <div class="col-md-2 col-sm-12 col-xs-12"></div>
         <div class="col-md-8 col-sm-12 col-xs-12 mts-section-header" style="padding-top:80px">
            <h2 class=" text-center">{!! $web_configuration->title_1 !!}</h2>
            <div class="text-left">
               {!! $web_configuration->text_1 !!}
            </div>
         </div>
         <div class="col-md-2 col-sm-12 col-xs-12"></div>
      </div>
   </div>
</section>
<section id="screenshot" class="">
   <div class="row blue-xouva" style="margin-right:0">
      <div class="col-md-12 col-sm-12 col-xs-12 mts-section-header">
      </div>
      <div class="col-md-3 col-sm-12 col-xs-12 mts-section-header">
         <i class="fas fa-map-marker-alt fa-2x" style="color:#00c4b3"></i>
         <a href="{{ setting('contact.location_url') }}" target="_blank">
            <p class="white">{{ setting('contact.location_name') }}</p>
         </a>
      </div>
      <div class="col-md-3 col-sm-12 col-xs-12 mts-section-header">
         <i class="fas fa-phone fa-2x" style="color:#00c4b3"></i> 
         <a href="tel:{{ setting('contact.phone') }}">
            <p class="white">{{ setting('contact.phone') }}</p>
         </a>
      </div>
      <div class="col-md-3 col-sm-12 col-xs-12 mts-section-header">
         <i class="fas fa-envelope fa-2x" style="color:#00c4b3"></i> 
         <p class="white"> <a href="mailto:info@xouvaboats.com" class="white">{{ setting('contact.commercial_information_email') }}</a><br>
            (@lang('messages.commercial_info'))
         </p>
      </div>
      <div class="col-md-3 col-sm-12 col-xs-12 mts-section-header">
         <i class="fas fa-envelope fa-2x" style="color:#00c4b3"></i> 
         <p class="white">  <a href="mailto:jose.ballester@xouvaboats.com" class="white">{{ setting('contact.technical_information_email') }}</a><br>
           (@lang('messages.technical_info'))
         </p>
      </div>
   </div>
</section>
<section class="bgc-one-top mts-section-wrapper mts-contact-section" data-stellar-background-ratio="0.5">
   <div class="container">
      <div class="row">
         <div class="mts-contact-details">
            <div class="col-md-2 col-sm-12 col-xs-12"></div>
            <div class="col-md-8 col-sm-12 col-xs-12 mts-contact-form">
               <div id="contact-result"></div>
               <div id="contact-form">
                  <form id="contact" action="/" method="POST">
                     {{ csrf_field() }}
                     <div class="mts-input-name mts-input-fields">
                        <input type="text" name="name" id="name" required="required" placeholder="@lang('messages.name')">
                     </div>
                     <div class="mts-input-email mts-input-fields">
                        <input type="email" name="email" id="email" required="required" placeholder="@lang('messages.email')">
                     </div>
                     <div class="mts-input-email mts-input-fields">
                        <input type="tel" name="phone" id="phone" required="required" placeholder="@lang('messages.phone')">
                     </div>
                     <div class="mts-input-message mts-input-fields">
                        <textarea name="message" id="message" required="required" cols="30" rows="10" placeholder="@lang('messages.message')"></textarea>
                     </div>
                     <input type="hidden" name="google_captcha_v3" value="" id="google_captcha_v3" />
                     <div id="send_form_button"></div>
                  </form>
               </div>
            </div>
            <div class="col-md-2 col-sm-12 col-xs-12"></div>
         </div>
      </div>
   </div>
</section>
<section>
   <div class="container" style="padding-bottom:50px">
      <div class="row">
         <div class="col-md-4 col-sm-12 col-xs-12 "> </div>
         <div class="col-md-4 col-sm-12 col-xs-12 "> 
            <img src="/storage/{!! $web_configuration->image_1 !!}" class="img-responsive" alt="{!! $web_configuration->image_1_alt !!}">
         </div>
         <div class="col-md-4 col-sm-12 col-xs-12 "> </div>
      </div>
   </div>
</section>
<div class="g-recaptcha" data-sitekey="{{ setting('site.captcha_key_client') }}"></div>
<script src="https://www.google.com/recaptcha/api.js?onload=ReCaptchaCallbackV3&render={{ setting('site.captcha_key_client') }}"></script>
<script>
    ReCaptchaCallbackV3 = function() {
        grecaptcha.ready(function() {
            grecaptcha.execute("{{ setting('site.captcha_key_client') }}").then(function(token) {
                $('#google_captcha_v3').val(token);
                $('#contact').attr('action', '/sendcontactmail');
                $('#send_form_button').append('<input style="background-color: #00c4b3;" type="submit" value="@lang('messages.send')" id="submit-btn">');
            });
        });
    };
</script>
@stop
```
Función en php

```
public function sendcontactmail(Request $request) {
    $request->validate([
        'name'=>'required',
        'email'=>'required',
        'phone'=>'required',
        'message'=>'required',
    ]);
    if($this->recaptchav3($request->input('google_captcha_v3')) > 0.7){
        $data = null;
        $data['name'] = $request->input('name');
        $data['email'] = $request->input('email');
        $data['phone'] = $request->input('phone');
        $data['content'] = $request->input('message');
        $contact_email = setting('contact.email');
        \Mail::to($contact_email)->bcc('pablo@primate.es')->send(new Contact($data));
        return redirect('/contact')->with('alert', 'Contact mail send successfully');
    } else {
        return redirect('/contact')->with('alert', 'Contact mail not send');
    }
}
public function recaptchav3(String $token = null) {
    $score = null;
    $response = (new \GuzzleHttp\Client())->request('post', 'https://www.google.com/recaptcha/api/siteverify', [
        'form_params' => [
            'response' => $token,
            'secret' => setting('site.captcha_key_server'),
        ],
    ]);
    $score = json_decode($response->getBody()->getContents(), true);
    return $score;
}
```
Ocultar el Badge que aparece abajo a la derecha con estilos

```
.grecaptcha-badge { visibility: hidden; }
```