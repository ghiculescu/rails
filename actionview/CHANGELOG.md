*   `check_box_tag` and `radio_button_tag` now accept `checked` as a keyword argument

    This is to make the API more consistent with the `FormHelper` variants. You can now provide `checked` as a positional or keyword argument:

    ```erb
    = check_box_tag "admin", "1", false
    = check_box_tag "admin", "1", checked: false

    = radio_button_tag 'favorite_color', 'maroon', false
    = radio_button_tag 'favorite_color', 'maroon', checked: false
    ```

    *Alex Ghiculescu*

*   Guard against `ActionView::Helpers::FormTagHelper#field_name` calls with nil
    `object_name` arguments. For example:

    ```erb
    <%= fields do |f| %>
      <%= f.field_name :body %>
    <% end %>
    ```

    *Sean Doyle*

*   Strings returned from `strip_tags` are correctly tagged `html_safe?`

    Because these strings contain no HTML elements and the basic entities are escaped, they are safe
    to be included as-is as PCDATA in HTML content. Tagging them as html-safe avoids double-escaping
    entities when being concatenated to a SafeBuffer during rendering.

    Fixes [rails/rails-html-sanitizer#124](https://github.com/rails/rails-html-sanitizer/issues/124)

    *Mike Dalessio*

*   Move `convert_to_model` call from `form_for` into `form_with`

    Now that `form_for` is implemented in terms of `form_with`, remove the
    `convert_to_model` call from `form_for`.

    *Sean Doyle*

*   Fix and add protections for XSS in `ActionView::Helpers` and `ERB::Util`.

    Escape dangerous characters in names of tags and names of attributes in the
    tag helpers, following the XML specification. Rename the option
    `:escape_attributes` to `:escape`, to simplify by applying the option to the
    whole tag.

    *Álvaro Martín Fraguas*

*   Extend audio_tag and video_tag to accept Active Storage attachments.

    Now it's possible to write

    ```ruby
    audio_tag(user.audio_file)
    video_tag(user.video_file)
    ```

    Instead of

    ```ruby
    audio_tag(polymorphic_path(user.audio_file))
    video_tag(polymorphic_path(user.video_file))
    ```

    `image_tag` already supported that, so this follows the same pattern.

    *Matheus Richard*

*   Ensure models passed to `form_for` attempt to call `to_model`.

    *Sean Doyle*

Please check [7-0-stable](https://github.com/rails/rails/blob/7-0-stable/actionview/CHANGELOG.md) for previous changes.
